# Guild of Shadows
- это приватный репозиторий, содержащий код и прочие ресурсы игры "Guild of Shadows" *(название рабочее)*.
Проект разрабатывается на игровом движке RGSS (Ruby Game Scripting System) на языке javascript.

### Репозиторий содержит:
* файлы кода;
* графические ресурсы;
* текст;
* Объекты движка;

### Примеры содержимого репозитория:

Пример кода:
```module Z05
  
  STEAL_SKILL = /<steal>/i
  STEAL_OBJ   = /<steal[:]*\s*(WEAPON|ITEM|ARMOR|GOLD)\s*(\d+)>/i
  
  NO_STEALS     = "%s has nothing to steal."
  STEAL_GOLD    = "Stole %s gold from %s."
  STEAL_ITEM    = "Stole %s from %s."
  
 end

class Window_BattleLog < Window_Selectable
  
  def display_steal(target)
    item = target.last_stolen_item
	print item;print "\n"
    if item.nil?
	  add_text(sprintf(Z05::NO_STEALS, target.name))
	  print "Nothing to Steal\n"
	elsif item.is_a?(Integer)
	  add_text(sprintf(Z05::STEAL_GOLD, item, target.name))
	  print "Stole #{item} Gold\n"
	else
	  add_text(sprintf(Z05::STEAL_ITEM, item.name, target.name))
	  print "Stole #{item.name}\n"
	end
	target.reset_steal_item
  end
  
  alias z05dd display_damage
  def display_damage(target, item)
    z05dd(target, item)
	display_steal(target) if item.steal?
  end
  
end

class RPG::UsableItem < RPG::BaseItem
  def steal?
    self.note.scan(Z05::STEAL_SKILL){return true}
	return false
  end
end

class Game_Enemy < Game_Battler
	attr_reader :last_stolen_item
  
  alias z05_initialize initialize
  def initialize(index, enemy_id)
    z05_initialize(index, enemy_id)
    z05_start
  end
  
  def z05_start
    @steal_data = []
    self.enemy.note.scan(Z05::STEAL_OBJ){|type, id|
      case type
      when /item/i
        @steal_data.push($data_items[id.to_i])
      when /weapon/i
        @steal_data.push($data_weapons[id.to_i])
      when /armor/i
        @steal_data.push($data_armors[id.to_i])
      when /gold/i
        @steal_data.push(id.to_i)
      end
    }
  end
  
  def apply_steal_effect
    return nil if @steal_data.size==0
    return @last_stolen_item=@steal_data.delete_at(rand(@steal_data.size))
  end
  
  def item_apply(user, item)
    super
	add_item_steal_effect if item.steal? unless @result.missed
  end
  
  def add_item_steal_effect
    @stolenitem = apply_steal_effect
	return if @stolenitem.nil?
	if @stolenitem.is_a?(Integer)
	  $game_party.gain_gold(@stolenitem)
	else
	  $game_party.gain_item(@stolenitem, 1)
	end
  end
  
  def reset_steal_item
    @last_stolen_item=nil
  end
  
end
```

Пример графического ресурса:
![Image](http://speed-new.com/wp-content/uploads/2015/11/24524526426.jpg)

## На какой стадии разработки находится проект?
Близок к завершению

## Кто занимается разработкой игры?
Разработкой занимаются 3 человека, среди них:
* Я - в качестве программиста;
* Николай - в качестве сценариста;
* Алина - в качестве худоника.

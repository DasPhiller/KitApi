# Usage

Here we want to take a look at how to use the api

## Creating a Kit

Start by creating a Kotlin class called "ExampleKit"
> **The name of the Class can be replaced by the name of your Kit**
>
{style="note"}

It should look like this

```Kotlin
   package com.example.kitapi.kits
   
   class ExampleKit {
   
   }
```

Now you implement a Kit

```Kotlin
package com.example.kitapi.kits
   
import de.dasphiller.kitapi.kit.*
   
class ExampleKit(
    override val description: Component = Component.text("Example Kit"),
    override val icon: Material = Material.DIAMOND_SWORD,
    override val name: String = "Example",
    override var cooldown: Double? = 20.0
) : Kit() {
   
}
```

This already defines name, description, icon and Cooldown of the Kit

Now lets give the Player a DIAMOND_SWORD

```Kotlin
    override fun enterArena(player: Player) {
        player.inventory.addItem(itemStack(Material.DIAMOND_SWORD) {
        })
    }
```

And if the Player jumps he gets a steak if he isn't on cooldown

```Kotlin
    private val jump = listen<PlayerJumpEvent> {
        val player = it.player
        if (!player.canUseKit()) return@listen
        if (player.kit == this) {
            player.inventory.addItem(ItemStack(Material.COOKED_BEEF))
            player.nextKitUse = cooldown?.toLong()!!
        }
    }
    
    override fun registerKit() {
        jump
    }
```

## Main Class

Your Main class should look like this
```Kotlin
package com.example.kitapi

import net.axay.kspigot.main.KSpigot
import de.dasphiller.kitapi.KitApi
import de.dasphiller.kitapi.kit.addKit

class ExamplePlugin: KSpigot() {

    override fun startup() {
        addKit(ExampleKit())
        kitApi.registerKits()        
    }
}

val kitApi get() = KitApi()
```

## Give a player a kit
Let's say when the Player joins the Server he gets our Kit 
We'll do this in our main class
```Kotlin
package com.example.kitapi

import net.axay.kspigot.main.KSpigot
import de.dasphiller.kitapi.KitApi
import de.dasphiller.kitapi.kit.addKit
import com.example.kitapi.kits.ExampleKit

class ExamplePlugin : KSpigot() {

    override fun startup() {
        addKit(ExampleKit())
        kitApi.registerKits()
        listen<PlayerJoinEvent> { 
            it.player.addToKit(ExampleKit())
        }        
    }
}

val kitApi get() = KitApi()
```

And we're done
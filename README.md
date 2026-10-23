LegacyJavaFixer
===============
This fixes a concurrent modification exception that is caused by the 
default implementation of Collections.sort being changed in https://bugs.openjdk.org/browse/JDK-8032636. 
This is not required on modern Forge versions, so verify before using.

Here is an example of the error fixed by this.
```ascii
[INFO] [ForgeModLoader] Calling tweak class cpw.mods.fml.common.launcher.FMLInjectionAndSortingTweaker
[SEVERE] [ForgeModLoader] Unable to launch
java.util.ConcurrentModificationException
	at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:911)
	at java.util.ArrayList$Itr.remove(ArrayList.java:875)
	at net.minecraft.launchwrapper.Launch.launch(Launch.java:114)
	at net.minecraft.launchwrapper.Launch.main(Launch.java:27)
	at net.minecraftforge.launcher.Main$Launcher.run(Main.java:282)
	at net.minecraftforge.launcher.Main$Launcher.access$000(Main.java:268)
	at net.minecraftforge.launcher.Main.main(Main.java:57)
```

To use this in production, just place the jar in your mods folder. It will be loaded as a CoreMod.

For dev time, it can be used by adding `net.minecraftforge.legacyjavafixer.LoadingPlugin` to the `fml.coreMods.load` environement variable.

FG7 example:
```groovy
minecraft {
    runs {
        configureEach {
            systemProperty 'fml.coreMods.load', 'net.minecraftforge.legacyjavafixer.LoadingPlugin'
        }
    }
}

dependencies {
    implementation 'net.minecraftforge:legacyjavafixer:2.0.1'
}
```


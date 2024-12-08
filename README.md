# Minecraft 1.0 Modding Guide: Using the ModInjector

## **Prerequisites**

Before we get started, make sure you have the following:

-   **Minecraft 1.0 (Java Edition)**: You need the version of Minecraft from 2011 (or the Minecraft 1.0 jar file).
-   **Java Development Kit (JDK)**: Java 8 (or higher) is required for compiling your code.
-   **A text editor or an IDE** (like IntelliJ IDEA or Eclipse) to write Java code.
-   **Basic knowledge of Java** (or a willingness to learn as you go).

----------

## **1. Setting Up Minecraft 1.0 and the ModInjector**

### **Step 1: Install Minecraft 1.0**

Make sure you have **Minecraft 1.0** installed on your system. If you don’t have it, you can download an old version of Minecraft from online archives or use the official Minecraft launcher to load version 1.0.

### **Step 2: Setting Up the Mod Injector**

The **ModInjector** is a custom tool that you will use to load your mods into Minecraft 1.0. It scans the `mods` folder inside your Minecraft installation, looks for `.zip` files, and then injects those mods into the game.

1.  **Download or Set Up the ModInjector**:
    
    -   If you haven’t already, create or download the `ModInjector.java` file we discussed earlier.
    -   The **ModInjector** scans for mods stored in a folder called `mods`, which should be inside your **.minecraft** folder.
2.  **Place ModInjector in Minecraft**:
    
    -   You need to ensure that the `ModInjector.java` file is part of your Minecraft codebase. This means integrating the `ModInjector` into the Minecraft source code, so it gets executed when the game starts.
3.  **Create the `mods` Folder**:
    
    -   Inside your `.minecraft` folder (which is located in your home directory), create a folder named `mods`. This is where you'll store all your mod `.zip` files.

----------

## **2. Creating Your First Mod**

Now that your **ModInjector** is set up, you can create your first mod!

### **Step 1: Write the Mod Code**

Your mod will consist of Java code that adds or modifies features in Minecraft. For simplicity, we'll write a basic mod that prints a message when it's loaded into the game.

Here’s the code for the mod:

```java
package com.example.mod;

public class ExampleMod {
    public static void load() {
        System.out.println("[ExampleMod] Mod loaded successfully!");
    }
}

```

### **Explanation of the Code**:

-   **package com.example.mod**: This defines the mod's package. Think of this as the folder structure that organizes the mod’s files.
-   **public class ExampleMod**: This is the main class of your mod. It contains the logic for what your mod will do.
-   **public static void load()**: This is the method that gets called when your mod is loaded. In this case, it just prints a message to the console.

### **Step 2: Compile Your Mod**

Once you’ve written the mod, you need to **compile** it. This turns your Java code into bytecode that Minecraft can understand.

-   You can use an IDE like **IntelliJ IDEA** or **Eclipse** to automatically compile the code.
-   Alternatively, if you're using the command line, you can use `javac` to compile the file.

For example, if you use `javac`, navigate to the directory where `ExampleMod.java` is located and run:

```sh
javac ExampleMod.java

```

This will create a `.class` file, which is the compiled version of your mod.

----------

### **Step 3: Package Your Mod into a ZIP File**

Minecraft mods need to be packaged into `.zip` files to be loaded by the `ModInjector`.

1.  **Create Folder Structure**:
    
    -   Create a folder named `com/example/mod/`.
    -   Place your compiled `ExampleMod.class` file inside that folder.
2.  **Zip the Folder**:
    
    -   Once the class file is in the correct folder, **zip** the folder into a `.zip` file.
    -   For example, you might have a file named `examplemod.zip`.

### **Step 4: Place Your Mod in the `mods` Folder**

-   Copy your `.zip` file (e.g., `examplemod.zip`) into the **`mods`** folder that you created earlier inside your **.minecraft** directory.

### **Step 5: Run Minecraft with ModInjector**

Now, run Minecraft with your `ModInjector` active.

1.  **Start Minecraft** as you normally would, but make sure the `ModInjector` is running in the background.
    
2.  **The ModInjector** will scan the `mods` folder and find `examplemod.zip`.
    
3.  The mod will be injected into the game, and it will print the following message in the Minecraft console:
    
    ```
    [ExampleMod] Mod loaded successfully!
    
    ```
    

Congrats! You’ve just created and loaded your first Minecraft mod!

----------

## **3. Expanding Your Mod: Adding Custom Items or Blocks**

Now that you know how to make a basic mod, let's see how you can expand it by adding custom items or blocks.

### **Adding a Custom Item**

Here’s an example of how to add a **custom item** to Minecraft:

```java
package com.example.mod;

import net.minecraft.src.Item;

public class ExampleMod {
    public static void load() {
        // Add a custom item with ID 1000
        Item customItem = new Item(1000);
        System.out.println("[ExampleMod] Custom item created!");
    }
}

```

This code adds a new item with ID `1000` to Minecraft.

### **Place the `.zip` File in the `mods` Folder** again

Once you’ve made changes, you need to recompile, zip, and place your updated mod file back into the `mods` folder.

When you run Minecraft again, it will load the updated mod and print:

```
[ExampleMod] Custom item created!

```

----------

## **4. Advanced Features: Reflection and Game Modification**

If you're looking to modify more advanced features, you can use **reflection** in Java to access Minecraft’s internal methods and change its behavior. This requires some deeper knowledge of how Minecraft works internally.

### Example: Using Reflection to Start the Game

```java
import java.lang.reflect.Method;
import net.minecraft.src.Minecraft;

public class ExampleMod {
    public static void load() {
        try {
            // Use reflection to access Minecraft's private methods
            Method method = Minecraft.class.getDeclaredMethod("startGame", null);
            method.setAccessible(true);
            method.invoke(Minecraft.getMinecraft(), null);
            System.out.println("[ExampleMod] Game started using reflection!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

This code uses **reflection** to call a private method (`startGame()`) in Minecraft and start the game. Reflection allows you to call methods that aren’t directly accessible, which can be useful for more advanced mods.

----------

## **5. Debugging and Troubleshooting**

If your mod isn't working, here are a few tips to help you troubleshoot:

-   **Check Minecraft’s console**: Minecraft will print any errors or issues related to loading your mod. This can help you understand what went wrong.
-   **Ensure the `.zip` file is in the right place**: Make sure your mod’s `.zip` file is in the `mods` folder and the structure is correct.
-   **Check the mod’s code**: If your mod isn't behaving as expected, review the code and ensure you're using the right methods or logic.

----------

## **Summary**

You’ve now learned how to:

1.  Set up **Minecraft 1.0** and **ModInjector**.
2.  Create a basic **Java mod** that prints a message when loaded into Minecraft.
3.  Expand your mod by adding custom items or blocks.
4.  Use advanced techniques like **reflection** to modify Minecraft’s behavior.

Modding in Minecraft 1.0 is a great way to learn how the game works and explore its inner mechanics. By following this guide, you should now be able to create, load, and test your own mods in Minecraft 1.0 using the **ModInjector**.

Let me know if you need help with more complex mods or run into any issues!

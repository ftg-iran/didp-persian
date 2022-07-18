# CATALOG OF DESIGN PATTERNS

## Creational Design Patterns


Cre­ation­al pat­terns pro­vide var­i­ous object cre­ation mech­a­nisms, which increase flex­i­bil­i­ty and reuse of exist­ing code.


> ### Fac­to­ry Method
> ![factory method](./images/cards/factory-method-mini.png)
>Pro­vides an inter­face for cre­at­ing objects in a super­class, but allows sub­class­es to alter the type of objects that will be cre­at­ed.

> ### Abstract Fac­to­ry
> ![Abstract Fac­to­ry](./images/cards/abstract-factory-mini.png)
>Lets you pro­duce fam­i­lies of relat­ed objects with­out spec­i­fy­ing their con­crete class­es.

> ### Builder
> ![builder](./images/cards/builder-mini.png)
>Lets you con­struct com­plex objects step by step. The pat­tern allows you to pro­duce dif­fer­ent types and rep­re­sen­ta­tions of an object using the same con­struc­tion code.

> ### Pro­to­type
> ![Pro­to­type](./images/cards/prototype-mini.png)
> Lets you copy exist­ing objects with­out mak­ing your code depen­dent on their class­es.

> ### Sin­gle­ton
> ![singleton](./images/cards/singleton-mini.png)
>Lets you ensure that a class has only one instance, while pro­vid­ing a glob­al access point to this instance.

---

![factory-method-en](./images/content/factory-method/factory-method-en.png)

## Factory Method
###### Also known as: Virtual Constructor


**Fac­to­ry Method** is a cre­ation­al design pat­tern that pro­vides an inter­face for cre­at­ing objects in a super­class, but allows sub­class­es to alter the type of objects that will be created.

### Prob­lem

Imag­ine that you’re cre­at­ing a logis­tics man­age­ment appli­ca­tion. The first ver­sion of your app can only han­dle trans­porta­tion by trucks, so the bulk of your code lives inside the Truck class.

After a while, your app becomes pret­ty pop­u­lar. Each day you receive dozens of requests from sea trans­porta­tion com­pa­nies to incor­po­rate sea logis­tics into the app.

![problem1-en](./images/diagrams/factory-method/problem1-en.png)

Adding a new class to the pro­gram isn’t that sim­ple if the rest of the code is already cou­pled to exist­ing classes.

Great news, right? But how about the code? At present, most of your code is cou­pled to the `Truck` class. Adding `Ships` into the app would require mak­ing changes to the entire code­base. More­over, if later you decide to add anoth­er type of trans­porta­tion to the app, you will prob­a­bly need to make all of these changes again.

As a result, you will end up with pret­ty nasty code, rid­dled with con­di­tion­als that switch the app’s behav­ior depend­ing on the class of trans­porta­tion objects.

### Solu­tion

The Fac­to­ry Method pat­tern sug­gests that you replace direct object con­struc­tion calls (using the new oper­a­tor) with calls to a spe­cial fac­to­ry method. Don’t worry: the objects are still cre­at­ed via the new oper­a­tor, but it’s being called from with­in the fac­to­ry method. Objects returned by a fac­to­ry method are often referred to as prod­ucts.

![solution1](./images/diagrams/factory-method/solution1.png)


Sub­class­es can alter the class of objects being returned by the fac­to­ry method.

At first glance, this change may look point­less: we just moved the con­struc­tor call from one part of the pro­gram to anoth­er. How­ev­er, con­sid­er this: now you can over­ride the fac­to­ry method in a sub­class and change the class of prod­ucts being cre­at­ed by the method.

There’s a slight lim­i­ta­tion though: sub­class­es may return dif­fer­ent types of prod­ucts only if these prod­ucts have a com­mon base class or inter­face. Also, the fac­to­ry method in the base class should have its return type declared as this interface.

![solution2-en](./images/diagrams/factory-method/solution2-en.png)

All prod­ucts must fol­low the same interface.

For exam­ple, both `Truck` and `Ship` class­es should imple­ment the `Transport` inter­face, which declares a method called `deliver`. Each class imple­ments this method dif­fer­ent­ly: trucks deliv­er cargo by land, ships deliv­er cargo by sea. The fac­to­ry method in the `RoadLogistics` class returns truck objects, where­as the fac­to­ry method in the `SeaLogistics` class returns ships.

The code that uses the fac­to­ry method (often called the client code) doesn’t see a dif­fer­ence between the actu­al prod­ucts returned by var­i­ous sub­class­es. The client treats all the prod­ucts as abstract `Transport`.

![Truck](./images/diagrams/factory-method/solution3-en.png)


As long as all prod­uct class­es imple­ment a com­mon inter­face, you can pass their objects to the client code with­out break­ing it.

The client knows that all trans­port objects are sup­posed to have the `deliver` method, but exact­ly how it works isn’t impor­tant to the client.


### Struc­ture

![structure-indexed](./images/diagrams/factory-method/structure-indexed.png)

1. The **Prod­uct** declares the inter­face, which is com­mon to all objects that can be pro­duced by the cre­ator and its subclasses

2. **Con­crete Prod­ucts** are dif­fer­ent imple­men­ta­tions of the prod­uct interface.

3. The **Cre­ator** class declares the fac­to­ry method that returns new prod­uct objects. It’s impor­tant that the return type of this method match­es the prod­uct interface.

You can declare the fac­to­ry method as abstract to force all sub­class­es to imple­ment their own ver­sions of the method. As an alter­na­tive, the base fac­to­ry method can return some default prod­uct type.

Note, despite its name, prod­uct cre­ation is **not** the pri­ma­ry respon­si­bil­i­ty of the cre­ator. Usu­al­ly, the cre­ator class already has some core busi­ness logic relat­ed to prod­ucts. The fac­to­ry method helps to decou­ple this logic from the con­crete prod­uct class­es. Here is an anal­o­gy: a large soft­ware devel­op­ment com­pa­ny can have a train­ing depart­ment for pro­gram­mers. How­ev­er, the pri­ma­ry func­tion of the com­pa­ny as a whole is still writ­ing code, not pro­duc­ing programmers.


4. **Con­crete Cre­ators** over­ride the base fac­to­ry method so it returns a dif­fer­ent type of product.


Note that the fac­to­ry method doesn’t have to **cre­ate** new instances all the time. It can also return exist­ing objects from a cache, an object pool, or anoth­er source.

### Pseudocode

This exam­ple illus­trates how the **Fac­to­ry Method** can be used for cre­at­ing cross-plat­form UI ele­ments with­out cou­pling the client code to con­crete UI classes.

The base dia­log class uses dif­fer­ent UI ele­ments to ren­der its win­dow. Under var­i­ous oper­at­ing sys­tems, these ele­ments may look a lit­tle bit dif­fer­ent, but they should still behave con­sis­tent­ly. A but­ton in Win­dows is still a but­ton in Linux.

![example](./images/diagrams/factory-method/example.png)

The cross-plat­form dia­log example.


When the fac­to­ry method comes into play, you don’t need to rewrite the logic of the dia­log for each oper­at­ing sys­tem. If we declare a fac­to­ry method that pro­duces but­tons inside the base dia­log class, we can later cre­ate a dia­log sub­class that returns Win­dows-styled but­tons from the fac­to­ry method. The sub­class then inher­its most of the dia­log’s code from the base class, but, thanks to the fac­to­ry method, can ren­der Win­dows-look­ing but­tons on the screen.

For this pat­tern to work, the base dia­log class must work with abstract but­tons: a base class or an inter­face that all con­crete but­tons fol­low. This way the dia­log’s code remains func­tion­al, whichev­er type of but­tons it works with.

Of course, you can apply this approach to other UI ele­ments as well. How­ev­er, with each new fac­to­ry method you add to the dia­log, you get clos­er to the **Abstract Fac­to­ry** pat­tern. Fear not, we’ll talk about this pat­tern later.

```c++
// The creator class declares the factory method that must
// return an object of a product class. The creator's subclasses
// usually provide the implementation of this method.
    class Dialog is
    // The creator may also provide some default implementation
    // of the factory method.
    abstract method createButton():Button

    // Note that, despite its name, the creator's primary
    // responsibility isn't creating products. It usually
    // contains some core business logic that relies on product
    // objects returned by the factory method. Subclasses can
    // indirectly change that business logic by overriding the
    // factory method and returning a different type of product
    // from it.
    method render() is
        // Call the factory method to create a product object.
        Button okButton = createButton()
        // Now use the product.
        okButton.onClick(closeDialog)
        okButton.render()


// Concrete creators override the factory method to change the
// resulting product's type.
class WindowsDialog extends Dialog is
    method createButton():Button is
        return new WindowsButton()


class WebDialog extends Dialog is
    method createButton():Button is
        return new HTMLButton()


// The product interface declares the operations that all
// concrete products must implement.
interface Button is
    method render()
    method onClick(f)

// Concrete products provide various implementations of the
// product interface.
class WindowsButton implements Button is
    method render(a, b) is
        // Render a button in Windows style.
    method onClick(f) is
        // Bind a native OS click event.


class HTMLButton implements Button is
    method render(a, b) is
        // Return an HTML representation of a button.
    method onClick(f) is
        // Bind a web browser click event.


class Application is
    field dialog: Dialog

    // The application picks a creator's type depending on the
    // current configuration or environment settings.
    method initialize() is

    config = readApplicationConfigFile()

    if (config.OS == "Windows") then
        dialog = new WindowsDialog()
    else if (config.OS == "Web") then
        dialog = new WebDialog()
    else
        throw new Exception("Error! Unknown operating system.")


// The client code works with an instance of a concrete
// creator, albeit through its base interface. As long as
// the client keeps working with the creator via the base
// interface, you can pass it any creator's subclass.

method main() is
    this.initialize()
    dialog.render()

```


### Applic­a­bil­i­ty


**Use the Fac­to­ry Method when you don’t know before­hand the exact types and depen­den­cies of the objects your code should work with.**


The Fac­to­ry Method sep­a­rates prod­uct con­struc­tion code from the code that actu­al­ly uses the prod­uct. There­fore it’s eas­i­er to extend the prod­uct con­struc­tion code inde­pen­dent­ly from the rest of the code.

For exam­ple, to add a new prod­uct type to the app, you’ll only need to cre­ate a new cre­ator sub­class and over­ride the fac­to­ry method in it.


**Use the Fac­to­ry Method when you want to pro­vide users of your library or frame­work with a way to extend its inter­nal components.**

Inher­i­tance is prob­a­bly the eas­i­est way to extend the default behav­ior of a library or frame­work. But how would the frame­work rec­og­nize that your sub­class should be used instead of a stan­dard com­po­nent?

The solu­tion is to reduce the code that con­structs com­po­nents across the frame­work into a sin­gle fac­to­ry method and let any­one over­ride this method in addi­tion to extend­ing the com­po­nent itself.

Let’s see how that would work. Imag­ine that you write an app using an open source UI frame­work. Your app should have round `but­tons`, but the frame­work only pro­vides square ones. You extend the stan­dard Button class with a glo­ri­ous `RoundButton` sub­class. But now you need to tell the main `UIFramework` class to use the new but­ton sub­class instead of a default one.

To achieve this, you cre­ate a sub­class `UIWithRoundButtons` from a base frame­work class and over­ride its `createButton` method. While this method returns `Button` objects in the base class, you make your sub­class return `RoundButton` objects. Now use the `UIWithRoundButtons` class instead of `UIFramework`. And that’s about it!

**Use the Fac­to­ry Method when you want to save sys­tem resources by reusing exist­ing objects instead of rebuild­ing them each time.**

You often expe­ri­ence this need when deal­ing with large, resource-inten­sive objects such as data­base con­nec­tions, file sys­tems, and net­work resources.

Let’s think about what has to be done to reuse an exist­ing object:


1. First, you need to cre­ate some stor­age to keep track of all of the cre­at­ed objects.

2. When some­one requests an object, the pro­gram should look for a free object inside that pool.

3. … and then return it to the client code.

4. If there are no free objects, the pro­gram should cre­ate a new one (and add it to the pool).

That’s a lot of code! And it must all be put into a sin­gle place so that you don’t pol­lute the pro­gram with dupli­cate code.

Prob­a­bly the most obvi­ous and con­ve­nient place where this code could be placed is the con­struc­tor of the class whose objects we’re try­ing to reuse. How­ev­er, a con­struc­tor must always return **new objects** by def­i­n­i­tion. It can’t return exist­ing instances.

There­fore, you need to have a reg­u­lar method capa­ble of cre­at­ing new objects as well as reusing exist­ing ones. That sounds very much like a fac­to­ry method.

### How to Imple­ment


1. Make all prod­ucts fol­low the same inter­face. This inter­face should declare meth­ods that make sense in every product.

2. Add an empty fac­to­ry method inside the cre­ator class. The return type of the method should match the com­mon prod­uct interface.

3. In the cre­ator’s code find all ref­er­ences to prod­uct con­struc­tors. One by one, replace them with calls to the fac­to­ry method, while extract­ing the prod­uct cre­ation code into the fac­to­ry method.

You might need to add a tem­po­rary para­me­ter to the fac­to­ry method to con­trol the type of returned product.

At this point, the code of the fac­to­ry method may look pret­ty ugly. It may have a large `switch` oper­a­tor that picks which prod­uct class to instan­ti­ate. But don’t worry, we’ll fix it soon enough.

4. Now, cre­ate a set of cre­ator sub­class­es for each type of prod­uct list­ed in the fac­to­ry method. Over­ride the fac­to­ry method in the sub­class­es and extract the appro­pri­ate bits of con­struc­tion code from the base method.

5. If there are too many prod­uct types and it doesn’t make sense to cre­ate sub­class­es for all of them, you can reuse the con­trol para­me­ter from the base class in subclasses.

For instance, imag­ine that you have the fol­low­ing hier­ar­chy of class­es: the base `Mail` class with a cou­ple of sub­class­es: `AirMail` and `GroundMail`; the `Transport` class­es are `Plane`, `Truck` and `Train`. While the `AirMail` class only uses Plane objects, `GroundMail` may work with both `Truck` and `Train` objects. You can cre­ate a new sub­class (say `TrainMail`) to han­dle both cases, but there’s anoth­er option. The client code can pass an argu­ment to the fac­to­ry method of the `GroundMail` class to con­trol which prod­uct it wants to receive.

6. If, after all of the extrac­tions, the base fac­to­ry method has become empty, you can make it abstract. If there’s some­thing left, you can make it a default behav­ior of the method.


### Pros and Cons

:heavy_check_mark: You avoid tight cou­pling between the cre­ator and the con­crete products.

:heavy_check_mark: Sin­gle Respon­si­bil­i­ty Prin­ci­ple. You can move the prod­uct cre­ation code into one place in the pro­gram, mak­ing the code eas­i­er to support.

:heavy_check_mark: Open/Closed Prin­ci­ple. You can intro­duce new types of prod­ucts into the pro­gram with­out break­ing exist­ing client code.

:heavy_multiplication_x: The code may become more com­pli­cat­ed since you need to intro­duce a lot of new sub­class­es to imple­ment the pat­tern. The best case sce­nario is when you’re intro­duc­ing the pat­tern into an exist­ing hier­ar­chy of cre­ator classes.

### Rela­tions with Other Pat­terns


- Many designs start by using **Fac­to­ry Method** (less com­pli­cat­ed and more cus­tomiz­able via sub­class­es) and evolve toward **Abstract Fac­to­ry**, **Pro­to­type**, or **Builder** (more flex­i­ble, but more complicated).

- **Abstract Fac­to­ry** class­es are often based on a set of **Fac­to­ry Meth­ods**, but you can also use **Pro­to­type** to com­pose the meth­ods on these classes.

- You can use **Fac­to­ry Method** along with **Iter­a­tor** to let col­lec­tion sub­class­es return dif­fer­ent types of iter­a­tors that are com­pat­i­ble with the collections.

- **Pro­to­type** isn’t based on inher­i­tance, so it doesn’t have its draw­backs. On the other hand, Pro­to­type requires a com­pli­cat­ed ini­tial­iza­tion of the cloned object. **Fac­to­ry Method** is based on inher­i­tance but doesn’t require an ini­tial­iza­tion step.

- **Fac­to­ry Method** is a spe­cial­iza­tion of **Tem­plate Method**. At the same time, a Fac­to­ry Method may serve as a step in a large Tem­plate Method.


    
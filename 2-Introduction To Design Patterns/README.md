# INTRODUCTION TO PATTERNS

## What's a Design Pattern?


**Design pat­terns** are typ­i­cal solu­tions to com­mon­ly occur­ring prob­lems in soft­ware design. They are like pre-made blue­prints that you can cus­tomize to solve a recur­ring design prob­lem in your code.

You can’t just find a pat­tern and copy it into your pro­gram, the way you can with off-the-shelf func­tions or libraries. The pat­tern is not a spe­cif­ic piece of code, but a gen­er­al con­cept for solv­ing a par­tic­u­lar prob­lem. You can fol­low the pat­tern details and imple­ment a solu­tion that suits the real­i­ties of your own program.

Pat­terns are often con­fused with algo­rithms, because both con­cepts describe typ­i­cal solu­tions to some known prob­lems. While an algo­rithm always defines a clear set of actions that can achieve some goal, a pat­tern is a more high-level descrip­tion of a solu­tion. The code of the same pat­tern applied to two dif­fer­ent pro­grams may be different.

An anal­o­gy to an algo­rithm is a cook­ing recipe: both have clear steps to achieve a goal. On the other hand, a pat­tern is more like a blue­print: you can see what the result and its fea­tures are, but the exact order of imple­men­ta­tion is up to you.

### What does the pat­tern con­sist of?


Most pat­terns are described very for­mal­ly so peo­ple can repro­duce them in many con­texts. Here are the sec­tions that are usu­al­ly present in a pat­tern description:


- **Intent** of the pat­tern briefly describes both the prob­lem and the solution.

- **Moti­va­tion** fur­ther explains the prob­lem and the solu­tion the pat­tern makes possible.

- **Struc­ture** of class­es shows each part of the pat­tern and how they are related.

- **Code exam­ple** in one of the pop­u­lar pro­gram­ming lan­guages makes it eas­i­er to grasp the idea behind the pattern.

Some pat­tern cat­a­logs list other use­ful details, such as applic­a­bil­i­ty of the pat­tern, imple­men­ta­tion steps and rela­tions with other patterns.

### Clas­si­fi­ca­tion of pat­terns

Design pat­terns dif­fer by their com­plex­i­ty, level of detail and scale of applic­a­bil­i­ty to the entire sys­tem being designed. I like the anal­o­gy to road con­struc­tion: you can make an inter­sec­tion safer by either installing some traf­fic lights or build­ing an entire multi-level inter­change with under­ground pas­sages for pedestrians.

The most basic and low-level pat­terns are often called idioms. They usu­al­ly apply only to a sin­gle pro­gram­ming language.

The most uni­ver­sal and high-level pat­terns are archi­tec­tur­al pat­terns. Devel­op­ers can imple­ment these pat­terns in vir­tu­al­ly any lan­guage. Unlike other pat­terns, they can be used to design the archi­tec­ture of an entire application.

In addi­tion, all pat­terns can be cat­e­go­rized by their intent, or pur­pose. This book cov­ers three main groups of patterns:

- **Cre­ation­al pat­terns** pro­vide object cre­ation mech­a­nisms that increase flex­i­bil­i­ty and reuse of exist­ing code.

- **Struc­tur­al pat­terns** explain how to assem­ble objects and class­es into larg­er struc­tures, while keep­ing the struc­tures flex­i­ble and efficient.

- **Behav­ioral pat­terns** take care of effec­tive com­mu­ni­ca­tion and the assign­ment of respon­si­bil­i­ties between objects.

### Who invent­ed pat­terns?

That’s a good, but not a very accu­rate, ques­tion. Design pat­terns aren’t obscure, sophis­ti­cat­ed con­cepts—quite the oppo­site. Pat­terns are typ­i­cal solu­tions to com­mon prob­lems in object-ori­ent­ed design. When a solu­tion gets repeat­ed over and over in var­i­ous projects, some­one even­tu­al­ly puts a name to it and describes the solu­tion in detail. That’s basi­cal­ly how a pat­tern gets discovered.

The con­cept of pat­terns was first described by Christo­pher Alexan­der in A Pat­tern Lan­guage: Towns, Build­ings, Con­struc­tion[^1]. The book describes a “lan­guage” for design­ing the urban envi­ron­ment. The units of this lan­guage are pat­terns. They may describe how high win­dows should be, how many lev­els a build­ing should have, how large green areas in a neigh­bor­hood are sup­posed to be, and so on.

The idea was picked up by four authors: Erich Gamma, John Vlis­sides, Ralph John­son, and Richard Helm. In 1994, they pub­lished Design Pat­terns: Ele­ments of Reusable Object-Ori­ent­ed Soft­ware[^2], in which they applied the con­cept of design pat­terns to pro­gram­ming. The book fea­tured 23 pat­terns solv­ing var­i­ous prob­lems of object-ori­ent­ed design and became a best-sell­er very quick­ly. Due to its lengthy name, peo­ple start­ed to call it “the book by the gang of four” which was soon short­ened to sim­ply “the GoF book”.

Since then, dozens of other object-ori­ent­ed pat­terns have been dis­cov­ered. The “pat­tern approach” became very pop­u­lar in other pro­gram­ming fields, so lots of other pat­terns now exist out­side of object-ori­ent­ed design as well.

## Why Should I Learn Patterns?


The truth is that you might man­age to work as a pro­gram­mer for many years with­out know­ing about a sin­gle pat­tern. A lot of peo­ple do just that. Even in that case, though, you might be imple­ment­ing some pat­terns with­out even know­ing it. So why would you spend time learn­ing them?

- Design pat­terns are a toolk­it of tried and test­ed solu­tions to com­mon prob­lems in soft­ware design. Even if you never encounter these prob­lems, know­ing pat­terns is still use­ful because it teach­es you how to solve all sorts of prob­lems using prin­ci­ples of object-ori­ent­ed design.

- Design pat­terns define a com­mon lan­guage that you and your team­mates can use to com­mu­ni­cate more effi­cient­ly. You can say, “Oh, just use a Sin­gle­ton for that,” and every­one will under­stand the idea behind your sug­ges­tion. No need to explain what a sin­gle­ton is if you know the pat­tern and its name.


[^1]: A Pattern Language: Towns, Buildings, Construction: https://refactoring.guru/pattern-language-book
[^2]: Design Patterns: Elements of Reusable Object-Oriented Software: https://refactoring.guru/gof-book
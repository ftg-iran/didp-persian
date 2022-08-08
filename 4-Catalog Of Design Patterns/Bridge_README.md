![bridge](./images/content/bridge/bridge.png)

## پُل

**پُل** یک الگوی طراحی ساختاریست که اجازه می‌دهد یک کلاس بزرگ یا مجموعه‌ای از کلاس‌های درهم تنیده به دو سلسله مراتب جدا تقسیم شوند - بخش انتزاع و پیاده‌سازی - که می‌توانند جداگانه توسعه داده شوند.

### :worried: مشکل

انتزاع؟ پیاده‌سازی؟ ترسناک به نظر می‌رسد؟ آرام باشید و اجازه دهید یک مثال ساده ببینیم.

فرض کنید یک کلاس به نام `shape` (شکل هندسی) به همراه دو زیرکلاس به نام‌های `Circle` (دایره) و `Square` (مربع) دارید. حالا می‌خواهید این کلاس را توسعه دهید تا با رنگ هم کار کند. پس می‌خواهید زیرکلاس‌های `Red` (قرمز) و `Blue` (آبی) را هم ایجاد کنید. ولی، از آنجا که قبلاً دو زیرکلاس داشتید، حالا باید چهار ترکیب از زیرکلاس‌ها بسازید مانند `BlueCircle` و `RedSquare`.

![problem-en](./images/diagrams/bridge/problem-en.png)

تعداد ترکیب‌های کلاس به شکل هندسی رشد می‌کند.

اضافه کردن شکل‌ها و رنگ‌های جدید، سلسله را به شکل نمایی بزرگ می‌کند. برای مثال، برای اضافه کردن شکل مثلث نیاز دارید که دو زیرکلاس ایجاد کنید، یک زیرکلاس برای هر رنگ. و بعد از آن، اضافه کردن یک رنگ جدید، نیاز به ساختن سه زیرکلاس خواهد داشت، یک زیرکلاس برای هر شکل. هر چه بیش‌تر جلو بروید، اوضاع بدتر می‌شود.

### :smiley: راه‌حل


این مشکل به این دلیل رخ می‌دهد که سعی می‌کنیم کلاس `shape` را در دو بُعد مستقل توسعه دهیم: بُعد شکل و رنگ. این یک مشکل بسیار رایج در ارث‌بری کلاس است.

الگوی پل سعی می‌کند این مشکل را با رها کردن ارث‌بری و استفاده از ترکیب اشیاء حل کند. این یعنی شما یکی از ابعاد را به یک سلسله‌ی جدا منتقل می‌کنید. حالا کلاس‌های اصلی، به یک شیء از سلسله‌ی جدید ارجاع می‌دهند به جای اینکه کل وضعیت و رفتارها را خودشان نگه دارند.

![solution-en](./images/diagrams/bridge/solution-en.png)

برای جلوگیری از انفجار سلسله‌ی کلاس می‌توان این سلسله را به چند سلسله‌ی مرتبط تبدیل کرد.

با دنبال کردن این راهبرد، می‌توان کُد مرتبط به رنگ را در کلاس خودش با دو زیرکلاسِ `Red` و `Blue` ذخیره کرد. به کلاس `Shape` یک فیلد ارجاع اضافه می‌شود که به یکی از اشیاء رنگ اشاره می‌کند. حالا کلاسِ شکل می‌تواند هر کار مربوط به رنگ را به شیءِ رنگِ مرتبط تفویض کند. این ارجاع مانند یک پل بین کلاس‌های `Shape` و `Color` عمل می‌کند. از حالا به بعد، اضافه کردن رنگ جدید، سلسله‌ی شکل را تغییر نمی‌دهد و اضافه کردن شکل جدید، سلسله‌ی رنگ را.

**انتزاع و پیاده‌سازی**


The GoF book[^1] introduces the terms Abstraction and Implementation as part of the Bridge definition. In my opinion, the terms sound too academic and make the pattern seem more complicated than it really is. Having read the simple example with shapes and colors, let’s decipher the meaning behind the GoF book’s scary words.

انتزاع (رابط یا interface هم گفته می‌شود) یک لایه‌ی کنترل سطح بالا برای برخی موجودیت‌ها است. این لایه قرار نیست خودش هیچ کار واقعی انجام دهد. تنها باید کار را به لایه‌ی پیاده‌سازی (پلتفرم هم گفته می‌شود) تفویض کند.

توجه کنید که درباره‌ی اینترفیس یا کلاس‌های انتزاعی زبان برنامه‌نویسی حرف نمی‌زنیم. این‌ها یکی نیستند.

داریم درباره‌ی برنامه‌های واقعی حرف می‌زنیم، لایه‌ی انتزاع می‌تواند توسط رابط کاربری گرافیکی (GUI) ارائه شود و لایه‌ی پیاده‌سازی می‌تواند کد سیستم عاملی باشد که GUI در پاسخ به کنش کاربر صدا می‌زند (API).

به شکل کلی، می‌توان چنین برنامه‌ای را در دو جهت مستقل گسترش داد:

- داشتن چند GUI متفاوت (برای مثال، GUIهای متفاوت برای مشتریان عادی و سرپرستان).

- پشتیبانی از APIهای مختلف (برای مثال، توانای اجرا روی ویندوز، لینوکس، و مک)

در حالت بدبینانه، این برنامه ممکن است مثل یک ظرف بزرگ ماکارونی به نظر برسد، جایی که صدها شرطْ انواع مختلف GUI را به انواع API وصل می‌کند.

![bridge-3-en](./images/content/bridge/bridge-3-en.png)

ایجاد یک تغییر ساده در یک کد یکپارچه بسیار سخت است. چون باید کل برنامه را خیلی خوب فهمیده باشید. تغییر دادن ماژول‌های کوچک‌تر و قابل فهم‌تر بسیار ساده‌تر است.

شما می‌توانید این آشوب را با انتقال کد ترکیب‌های اینترفیس و پلتفرم به کلاس‌های جداگانه منظم کنید. ولی، به زودی خواهید دید که تعداد زیادی از این کلاس‌ها به وجود آمده‌اند. سلسله‌ی کلاس‌ها به صورت نمایی رشد می‌کند چون اضافه کردن یک GUI جدید یا پشتیبانی یک API متفاوت نیاز به ساخت کلاس‌های بیش‌تر و بیش‌تر دارد.

اجازه دهید این مشکل را با الگوی پل حل کنیم. این الگو پیشنهاد می‌دهد کلاس‌ها را به دو سلسله‌ی مجزا تقسیم کنیم:

- انتزاع: لایه‌ی GUI برنامه

- پیاده‌سازی: API سیستم‌عامل

![bridge-2-en](./images/content/bridge/bridge-2-en.png)

یکی از راه‌های ساختار بخشی به برنامه‌ی چند پلتفرمی

شیء انتزاع ظاهر برنامه را کنترل می‌کند و کار اصلی را به شیءِ پیاده‌سازی متصل تفویض می‌کند. پیاده‌سازی‌های مختلف قابل جایگزینی هستند، تا زمانی که از یک اینترفیس یکسان استفاده می‌کنند. به این شکل، یک GUI می‌تواند روی ویندوز و لینوکس کار کند.

طبیعتاً، می‌توان کلاس‌های GUI را بدون تغییر کلاس‌های مربوط به API عوض کرد. حتی بهتر، اضافه کردن پشتیبانی برای یک سیستم‌عاملِ دیگر تنها نیاز به ایجاد یک زیرکلاس در بخش پیاده‌سازی دارد.

### :construction: ساختار

![structure-en-indexed](./images/diagrams/bridge/structure-en-indexed.png)

1. **بخش انتزاع** منطق سطح بالا را فراهم می‌کند و به شیء پیاده‌سازی برای انجام کار اصلی متکی است.

2. The **Implementation** declares the interface that’s common for all concrete implementations. An abstraction can only communicate with an implementation object via methods that are declared here.
The abstraction may list the same methods as the implementation, but usually the abstraction declares some complex behaviors that rely on a wide variety of primitive operations declared by the implementation.

3. Concrete Implementations contain platform-specific code.

4. **انتزاع تصحیح** شده انواعی از منطق کنترل را فراهم می‌کند و مانند والدش، با پیاده‌سازی‌های متفاوتی به وسیله‌ی اینترفیسِ عمومیِ پیاده‌سازی کار می‌کند.

5. Usually, the **Client** is only interested in working with the abstraction. However, it’s the client’s job to link the abstraction object with one of the implementation objects.

### :hash: شبه‌کد

این مثال نشان می‌دهد که چگونه **الگوی پل** به جدا کردن کدِ یکپارچه‌ی یک برنامه که چند دستگاه و کنترل از راه دورشان (remote control) را کنترل می‌کند، کمک می‌کند. کلاس‌های `Device` به عنوان پیاده‌سازی عمل می‌کنند و کلاس‌های `Remote` نقش انتزاع را بازی می‌کنند.

کلاس پایه‌ی ریموت دور یک فیلد ارجاع تعریف می‌کند که کلاس را به شیءِ دستگاه وصل می‌کند. همه‌ی ریموت‌ها به وسیله‌ی اینترفیس عمومی دستگاهْ با دستگاه‌ها رابطه برقرار می‌کنند. این موضوع به ریموت اجازه می‌دهد با چند نوع دستگاه کار کند.

![example-en](./images/diagrams/bridge/example-en.png)

سلسله‌ی اصلی کلاس‌ها به دو بخش تقسیم شده: دستگاه‌ها و کنترل از راه دورها

می‌توان کلاس‌های ریموت را مستقل از کلاس‌های دستگاه‌ها توسعه داد. تمام چیزی که نیاز است، ساختن یک زیرکلاس جدیدِ ریموت است. برای نمونه، یک ریموت ابتدایی می‌تواند دو دکمه داشته باشد، اما می‌تواند با امکانات جدید، مثل باتری اضافه یا صفحه‌ی لمسی توسعه پیدا کند.

The client code links the desired type of remote control with a specific device object via the remote’s constructor.

```c++
// The "abstraction" defines the interface for the "control"
// part of the two class hierarchies. It maintains a reference
// to an object of the "implementation" hierarchy and delegates
// all of the real work to this object.
class RemoteControl is
    protected field device: Device
    constructor RemoteControl(device: Device) is
        this.device = device
    method togglePower() is
        if (device.isEnabled()) then
            device.disable()
    else
            device.enable()
    method volumeDown() is
        device.setVolume(device.getVolume() - 10)
    method volumeUp() is
        device.setVolume(device.getVolume() + 10)
    method channelDown() is
        device.setChannel(device.getChannel() - 1)
    method channelUp() is
        device.setChannel(device.getChannel() + 1)


// You can extend classes from the abstraction hierarchy
// independently from device classes.
class AdvancedRemoteControl extends RemoteControl is
    method mute() is
        device.setVolume(0)


// The "implementation" interface declares methods common to all
// concrete implementation classes. It doesn't have to match the
// abstraction's interface. In fact, the two interfaces can be
// entirely different. Typically the implementation interface
// provides only primitive operations, while the abstraction
// defines higher-level operations based on those primitives.
interface Device is
    method isEnabled()
    method enable()
    method disable()
    method getVolume()
    method setVolume(percent)
    method getChannel()
    method setChannel(channel)


// All devices follow the same interface.
class Tv implements Device is
    // ...

class Radio implements Device is
    // ...


// Somewhere in client code.
tv = new Tv()
remote = new RemoteControl(tv)
remote.togglePower()

radio = new Radio()
remote = new AdvancedRemoteControl(radio)

```

### :bulb: قابلیت اجرا

:beetle: **از الگوی پل زمانی استفاده کنید که می‌خواهید یک کلاس یکپارچه که انواع مختلفی از چند کارکرد دارد (برای مثال، کلاس می‌تواند با انواع سرورهای پایگاه داده کار کند) را تقسیم و ساماندهی کنید.**

:sparkles: The bigger a class becomes, the harder it is to figure out how it works, and the longer it takes to make a change. The changes made to one of the variations of functionality may require making changes across the whole class, which often results in making errors or not addressing some critical side effects.

الگوی پل به شما اجازه می‌دهد کلاس یکپارچه را به چند سلسله کلاس تقسیم کنید. بعد از این می‌توانید کلاس‌های هر سلسله را مستقل از کلاس‌های دیگر تغییر دهید. این رویکرد نگهداری کد را ساده و ریسک خراب کردن کد را کمینه می‌کند.

:beetle: **از این الگو زمانی استفاده کنید که نیاز دارید یک کلاس را در چند جهتِ مستقل گسترش دهید.**

:sparkles: الگوی پل پیشنهاد می‌کند که برای هر بُعد، یک سلسله کلاس جدا داشته باشید. کلاس اصلی کارِ مرتبط را به اشیاءِ آن سلسله‌ها تفویض می‌کند به جای اینکه خودش همه‌ی کارها را انجام دهد.

:beetle: **از الگوی پل استفاده کنید اگر باید بتوانید در زمان اجرای برنامه از پیاده‌سازی‌های مختلف استفاده کنید.**

:sparkles: Although it’s optional, the Bridge pattern lets you replace the implementation object inside the abstraction. It’s as easy as assigning a new value to a field.

این آیتم آخر دلیل اصلی این است که بسیاری از مردم الگوی پل را با الگوی استراتژی اشتباه می‌گیرند. به یاد داشته باشید که یک الگو چیزی بیش‌تر از روش خاصی برای ساختار دادن به کلاس‌های شما است. یک الگو می‌تواند نیات و مشکلات را هم ابراز کند.




### :clipboard: چگونگی اجرا

1. ابعاد مستقل در کلاس‌ها را شناسایی کنید. این مفاهیم مستقل می‌توانند این‌ها باشند:
   1. انتزاع / بستر
   2. دامنه / زیرساخت
   3. فرانت‌اِند / بک‌اِند
   4. اینترفیس / پیاده‌سازی
2. See what operations the client needs and define them in the base abstraction class.
3. بررسی کنید عملیات‌ها روی تمام پلتفرم‌ها در دسترس هستند. عملیات‌هایی که بخش انتزاع در اینترفیس عمومی نیاز دارد را در تعریف کنید.
4. For all platforms in your domain create concrete implementation classes, but make sure they all follow the implementation interface.
5. درون کلاس انتزاع یک فیلد ارجاع برای نوع پیاده‌سازی اضافه کنید. انتزاع بیش‌تر کارها را به شیءِ پیاده‌سازی که در این فیلد ارجاع شده تفویض می‌کند.
6. If you have several variants of high-level logic, create refined abstractions for each variant by extending the base abstraction class.
7. The client code should pass an implementation object to the abstraction’s constructor to associate one with the other. After that, the client can forget about the implementation and work only with the abstraction object.

### ⚖️ معایب و مزایا

:heavy_check_mark: توانایی ساخت برنامه‌ها و کلاس‌های مستقل از پلتفرم

:heavy_check_mark: The client code works with high-level abstractions. It isn’t exposed to the platform details.

:heavy_check_mark: Open/Closed Principle. You can introduce new abstractions and implementations independently from each other.

:heavy_check_mark: Single Responsibility Principle. You can focus on high-level logic in the abstraction and on platform details in the implementation.

:heavy_multiplication_x: ممکن است با انجام این الگو روی یک کلاس چسبنده (cohesive) کد پیچیده‌تر شود.


### :arrows_counterclockwise: Relations with Other Patterns

- **Bridge** is usually designed up-front, letting you develop parts of an application independently of each other. On the other hand, **Adapter** is commonly used with an existing app to make some otherwise-incompatible classes work together nicely.

- **Bridge**, **State**, **Strategy** (and to some degree **Adapter**) have very similar structures. Indeed, all of these patterns are based on composition, which is delegating work to other objects. However, they all solve different problems. A pattern isn’t just a recipe for structuring your code in a specific way. It can also communicate to other developers the problem the pattern solves.

- You can use **Abstract Factory** along with **Bridge**. This pairing is useful when some abstractions defined by Bridge can only work with specific implementations. In this case, Abstract Factory can encapsulate these relations and hide the complexity from the client code.

- You can combine **Builder** with **Bridge**: the director class plays the role of the abstraction, while different builders act as implementations.

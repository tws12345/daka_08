# daka_08
模块与datetime模块

模块

    在前面我们脚本是用 Python 解释器来编程，如果你从 Python 解释器退出再进入，那么你定义的所有的方法和变量就都消失了。

    为此 Python 提供了一个办法，把这些定义存放在文件中，为一些脚本或者交互式的解释器实例使用，这个文件被称为模块（Module）。

    模块是一个包含所有你定义的函数和变量的文件，其后缀名是.py。模块可以被别的程序引入，以使用该模块中的函数等功能。这也是使用 Python 标准库的方法。

1.什么是模块

    容器 -> 数据的封装
    函数 -> 语句的封装
    类 -> 方法和属性的封装
    模块 -> 程序文件
    创建一个 hello.py 文件

    # hello.py
    def hi():
        print('Hi everyone, I love lsgogroup!')
    
2.命名空间

    命名空间因为对象的不同，也有所区别，可以分为如下几种：

    内置命名空间（Built-in Namespaces）：
    全局命名空间（Module：Global Namespaces）：
    本地命名空间（Function & Class：Local Namespaces）：



    程序在查询上述三种命名空间的时候，就按照从里到外的顺序


    import hello

    hello.hi()  # Hi everyone, I love lsgogroup!
    hi()  # NameError: name 'hi' is not defined

3.导入模块

    创建一个模块 TemperatureConversion.py

    # TemperatureConversion.py
    def c2f(cel):
        fah = cel * 1.8 + 32
        return fah


    def f2c(fah):
        cel = (fah - 32) / 1.8
        return cel
    第一种：import 模块名


    import TemperatureConversion

    print('32摄氏度 = %.2f华氏度' % TemperatureConversion.c2f(32))
    print('99华氏度 = %.2f摄氏度' % TemperatureConversion.f2c(99))

    # 32摄氏度 = 89.60华氏度
    # 99华氏度 = 37.22摄氏度

    第二种：from 模块名 import 函数名


    from TemperatureConversion import c2f, f2c

    print('32摄氏度 = %.2f华氏度' % c2f(32))
    print('99华氏度 = %.2f摄氏度' % f2c(99))

    # 32摄氏度 = 89.60华氏度
    # 99华氏度 = 37.22摄氏度

    第三种：import 模块名 as 新名字


    import TemperatureConversion as tc

    print('32摄氏度 = %.2f华氏度' % tc.c2f(32))
    print('99华氏度 = %.2f摄氏度' % tc.f2c(99))

    # 32摄氏度 = 89.60华氏度
    # 99华氏度 = 37.22摄氏度

4.if __name__ == '__main__'

      对于很多编程语言来说，程序都必须要有一个入口，而 Python 则不同，它属于脚本语言，不像编译型语言那样先将程序编译成二进制再运行，
      而是动态的逐行解释运行。也就是从脚本第一行开始运行，没有统一的入口。

      假设我们有一个 const.py 文件，内容如下：

      PI = 3.14


      def main():
          print("PI:", PI)


      main()

      # PI: 3.14
      现在，我们写一个用于计算圆面积的 area.py 文件，area.py 文件需要用到 const.py 文件中的 PI 变量。从 const.py 中，我们把 PI 变量导入 area.py：

      from const import PI


      def calc_round_area(radius):
          return PI * (radius ** 2)


      def main():
          print("round area: ", calc_round_area(2))


      main()

      '''
      PI: 3.14
      round area:  12.56
      '''
      我们看到 const.py 中的 main 函数也被运行了，实际上我们不希望它被运行，因为 const.py 提供的 main 函数只是为了测试常量定义。这时if __name__ == '__main__'派上了用场，我们把 const.py 改一下，添加if __name__ == "__main__"：

      PI = 3.14

      def main():
          print("PI:", PI)

      if __name__ == "__main__":
          main()
      运行 const.py，输出如下：

      PI: 3.14
      运行 area.py，输出如下：

      round area:  12.56
      __name__：是内置变量，可用于表示当前模块的名字。

      import const

      print(__name__)
      # __main__

      print(const.__name__)
      # const
      由此我们可知：如果一个 .py 文件（模块）被直接运行时，其__name__值为__main__，即模块名为__main__。

      所以，if __name__ == '__main__'的意思是：当 .py 文件被直接运行时，if __name__ == '__main__'之下的代码块将被运行；当 .py 文件以模块形式被导入时，if __name__ == '__main__'之下的代码块不被运行。

5.搜索路径

    当解释器遇到 import 语句，如果模块在当前的搜索路径就会被导入。



    import sys

    print(sys.path)

    # ['C:\\ProgramData\\Anaconda3\\DLLs', 'C:\\ProgramData\\Anaconda3\\lib', 'C:\\ProgramData\\Anaconda3', 'C:\\ProgramData\\Anaconda3\\lib\\site-packages',...]
    我们使用 import 语句的时候，Python 解释器是怎样找到对应的文件的呢？

    这就涉及到 Python 的搜索路径，搜索路径是由一系列目录名组成的，Python 解释器就依次从这些目录中去寻找所引入的模块。

    这看起来很像环境变量，事实上，也可以通过定义环境变量的方式来确定搜索路径。

    搜索路径是在 Python 编译或安装的时候确定的，安装新的库应该也会修改。搜索路径被存储在 sys 模块中的 path 变量中。

6.包（package）

    包是一种管理 Python 模块命名空间的形式，采用"点模块名称"。

    创建包分为三个步骤：

    创建一个文件夹，用于存放相关的模块，文件夹的名字即包的名字。
    在文件夹中创建一个 __init__.py 的模块文件，内容可以为空。
    将相关的模块放入文件夹中。
    不妨假设你想设计一套统一处理声音文件和数据的模块（或者称之为一个"包"）。

    现存很多种不同的音频文件格式（基本上都是通过后缀名区分的，例如： .wav，.aiff，.au），所以你需要有一组不断增加的模块，用来在不同的格式之间转换。

    并且针对这些音频数据，还有很多不同的操作（比如混音，添加回声，增加均衡器功能，创建人造立体声效果），所以你还需要一组怎么也写不完的模块来处理这些操作。

    这里给出了一种可能的包结构（在分层的文件系统中）:

    sound/                          顶层包
          __init__.py               初始化 sound 包
          formats/                  文件格式转换子包
                  __init__.py
                  wavread.py
                  wavwrite.py
                  aiffread.py
                  aiffwrite.py
                  auread.py
                  auwrite.py
                  ...
          effects/                  声音效果子包
                  __init__.py
                  echo.py
                  surround.py
                  reverse.py
                  ...
          filters/                  filters 子包
                  __init__.py
                  equalizer.py
                  vocoder.py
                  karaoke.py
                  ...
    在导入一个包的时候，Python 会根据 sys.path 中的目录来寻找这个包中包含的子目录。

    目录只有包含一个叫做 __init__.py 的文件才会被认作是一个包，最简单的情况，放一个空的 __init__.py 就可以了。

    import sound.effects.echo
    这将会导入子模块 sound.effects.echo。 他必须使用全名去访问:

    sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
    还有一种导入子模块的方法是：

    from sound.effects import echo
    这同样会导入子模块: echo，并且他不需要那些冗长的前缀，所以他可以这样使用：

    echo.echofilter(input, output, delay=0.7, atten=4)
    还有一种变化就是直接导入一个函数或者变量：

    from sound.effects.echo import echofilter
    同样的，这种方法会导入子模块: echo，并且可以直接使用他的 echofilter() 函数：

    echofilter(input, output, delay=0.7, atten=4)
    注意当使用 from package import item 这种形式的时候，对应的 item 既可以是包里面的子模块（子包），或者包里面定义的其他名称，比如函数，类或者变量。

    设想一下，如果我们使用 from sound.effects import * 会发生什么？

    Python 会进入文件系统，找到这个包里面所有的子模块，一个一个的把它们都导入进来。

    导入语句遵循如下规则：如果包定义文件 __init__.py 存在一个叫做 __all__ 的列表变量，那么在使用 from package import * 的时候就把这个列表中的所有名字作为包内容导入。

    这里有一个例子，在 sounds/effects/__init__.py中包含如下代码：

    __all__ = ["echo", "surround", "reverse"]
    这表示当你使用 from sound.effects import *这种用法时，你只会导入包里面这三个子模块。

    如果 __all__ 真的没有定义，那么使用from sound.effects import *这种语法的时候，就不会导入包 sound.effects 里的任何子模块。他只是把包 sound.effects 和它里面定义的所有内容导入进来（可能运行__init__.py里定义的初始化代码）。

    这会把 __init__.py 里面定义的所有名字导入进来。并且他不会破坏掉我们在这句话之前导入的所有明确指定的模块。

    import sound.effects.echo
    import sound.effects.surround
    from sound.effects import *
    这个例子中，在执行 from...import 前，包 sound.effects 中的 echo 和 surround 模块都被导入到当前的命名空间中了。

    通常我们并不主张使用 * 这种方法来导入模块，因为这种方法经常会导致代码的可读性降低。


练习题：

    1、怎么查出通过 from xx import xx导⼊的可以直接调⽤的⽅法？
            可以用dir()来返回这个包
            >>> import math
            >>> dir(math)
            ['__doc__', '__loader__', '__name__', '__package__', '__spec__', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'copysign', 'cos', 'cosh', 'degrees', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'gcd', 'hypot', 'inf', 'isclose', 'isfinite', 'isinf', 'isnan', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'log2', 'modf', 'nan', 'pi', 'pow', 'radians', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'tau', 'trunc']

    2、了解Collection模块，编写程序以查询给定列表中最常见的元素。

    题目说明：

    输入：language = ['PHP', 'PHP', 'Python', 'PHP', 'Python', 'JS', 'Python', 'Python','PHP', 'Python']

    输出：Python

    """
    Input file
    language = ['PHP', 'PHP', 'Python', 'PHP', 'Python', 'JS', 'Python', 'Python','PHP', 'Python']

    Output file
    Python
    """
    def most_element(language):
        """ Return a list of lines after inserting a word in a specific line. """

        # your code here
        from collections import Counter

        language = ['PHP', 'PHP', 'Python', 'PHP', 'Python', 'JS', 'Python', 'Python','PHP', 'Python']

        def most_element(language):
          cnt=Counter()
          for lg in language :
              cnt[lg]+=1
          return sorted(list(cnt.items()), key = lambda x:x[1])[-1][0]

        In [2]: most_element(language)
        Out[2]: 'Python'


datetime模块

    datetime 是 Python 中处理日期的标准模块，它提供了 4 种对日期和时间进行处理的类：datetime、date、time 和 timedelta。

1.datetime类

    datetime.now(tz=None) 获取当前的日期时间，输出顺序为：年、月、日、时、分、秒、微秒。
    datetime.timestamp() 获取以 1970年1月1日为起点记录的秒数。
    datetime.fromtimestamp(tz=None) 使用 unixtimestamp 创建一个 datetime。

    如何创建一个 datetime 对象？

    import datetime

    dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=23, second=59)
    print(dt)  # 2020-06-25 11:23:59
    print(dt.timestamp())  # 1593055439.0

    dt = datetime.datetime.fromtimestamp(1593055439.0)
    print(dt)  # 2020-06-25 11:23:59
    print(type(dt)) # <class 'datetime.datetime'>

    dt = datetime.datetime.now()
    print(dt)  # 2020-06-25 11:11:03.877853
    print(type(dt))  # <class 'datetime.datetime'>
    datetime.strftime(fmt) 格式化 datetime 对象。
    符号	说明
    %a	本地简化星期名称（如星期一，返回 Mon）
    %A	本地完整星期名称（如星期一，返回 Monday）
    %b	本地简化的月份名称（如一月，返回 Jan）
    %B	本地完整的月份名称（如一月，返回 January）
    %c	本地相应的日期表示和时间表示
    %d	月内中的一天（0-31）
    %H	24小时制小时数（0-23）
    %I	12小时制小时数（01-12）
    %j	年内的一天（001-366）
    %m	月份（01-12）
    %M	分钟数（00-59）
    %p	本地A.M.或P.M.的等价符
    %S	秒（00-59）
    %U	一年中的星期数（00-53）星期天为星期的开始
    %w	星期（0-6），星期天为星期的开始
    %W	一年中的星期数（00-53）星期一为星期的开始
    %x	本地相应的日期表示
    %X	本地相应的时间表示
    %y	两位数的年份表示（00-99）
    %Y	四位数的年份表示（0000-9999）
    %Z	当前时区的名称（如果是本地时间，返回空字符串）
    %%	%号本身

    如何将 datetime 对象转换为任何格式的日期？

    import datetime

    dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=51, second=49)
    s = dt.strftime("'%Y/%m/%d %H:%M:%S")
    print(s)  # '2020/06/25 11:51:49

    s = dt.strftime('%d %B, %Y, %A')
    print(s)  # 25 June, 2020, Thursday

    如何将给定日期转换为 "mmm-dd, YYYY" 的格式？

    # 输入
    d1 = datetime.date('2010-09-28')

    # 输出
    'Sep-28,2010'


    import datetime

    d1 = datetime.date(2010, 9, 28)
    print(d1.strftime('%b-%d,%Y'))
    # Sep-28,2010
    datetime.date() Return the date part.
    datetime.time() Return the time part, with tzinfo None.
    datetime.year 年
    datetime.month 月
    datetime.day 日
    datetime.hour 小时
    datetime.minute 分钟
    datetime.second 秒
    datetime.isoweekday 星期几

    datetime 对象包含很多与日期时间相关的实用功能。

    import datetime

    dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=51, second=49)
    print(dt.date())  # 2020-06-25
    print(type(dt.date()))  # <class 'datetime.date'>
    print(dt.time())  # 11:51:49
    print(type(dt.time()))  # <class 'datetime.time'>
    print(dt.year)  # 2020
    print(dt.month)  # 6
    print(dt.day)  # 25
    print(dt.hour)  # 11
    print(dt.minute)  # 51
    print(dt.second)  # 49
    print(dt.isoweekday())  # 4
    在处理含有字符串日期的数据集或表格时，我们需要一种自动解析字符串的方法，无论它是什么格式的，都可以将其转化为 datetime 对象。这时，就要使用到 dateutil 中的 parser 模块。

    parser.parse(timestr, parserinfo=None, **kwargs)

    如何在 python 中将字符串解析为 datetime对象？

    from dateutil import parser

    s = '2020-06-25'
    dt = parser.parse(s)
    print(dt)  # 2020-06-25 00:00:00
    print(type(dt))  # <class 'datetime.datetime'>

    s = 'March 31, 2010, 10:51pm'
    dt = parser.parse(s)
    print(dt)  # 2010-03-31 22:51:00
    print(type(dt))  # <class 'datetime.datetime'>

    如何将字符串日期解析为 datetime 对象？

    # 输入
    s1 = "2010 Jan 1"
    s2 = '31-1-2000'
    s3 = 'October10, 1996, 10:40pm'

    # 输出
    2010-01-01 00:00:00
    2000-01-31 00:00:00
    2019-10-10 22:40:00


    from dateutil import parser

    s1 = "2010 Jan 1"
    s2 = '31-1-2000'
    s3 = 'October10, 1996, 10:40pm'

    dt1 = parser.parse(s1)
    dt2 = parser.parse(s2)
    dt3 = parser.parse(s3)

    print(dt1)  # 2010-01-01 00:00:00
    print(dt2)  # 2000-01-31 00:00:00
    print(dt3)  # 1996-10-10 22:40:00

    计算以下列表中连续的天数。

    # 输入
    ['Oct, 2, 1869', 'Oct, 10, 1869', 'Oct, 15, 1869', 'Oct, 20, 1869','Oct, 23, 1869']

    # 输出
    [8, 5, 5, 3]


    import numpy as np
    from dateutil import parser

    dateString = ['Oct, 2, 1869', 'Oct, 10, 1869', 'Oct, 15, 1869', 'Oct, 20, 1869', 'Oct, 23, 1869']
    dates = [parser.parse(i) for i in dateString]
    td = np.diff(dates)
    print(td)
    # [datetime.timedelta(days=8) datetime.timedelta(days=5)
    #  datetime.timedelta(days=5) datetime.timedelta(days=3)]
    d = [i.days for i in td]
    print(d)  # [8, 5, 5, 3]

2.date类
    class date:
        def __init__(self, year, month, day):
            pass
        def today(cls):
            pass
    date.today() 获取当前日期信息。

    如何在 Python 中获取当前日期和时间？

    import datetime

    d = datetime.date(2020, 6, 25)
    print(d)  # 2020-06-25
    print(type(d))  # <class 'datetime.date'>

    d = datetime.date.today()
    print(d)  # 2020-06-25
    print(type(d))  # <class 'datetime.date'>

    如何统计两个日期之间有多少个星期六？

    # 输入
    d1 = datetime.date(1869, 1, 2)
    d2 = datetime.date(1869, 10, 2)

    # 输出
    40


    import datetime

    d1 = datetime.date(1869, 1, 2)
    d2 = datetime.date(1869, 10, 2)
    dt = (d2 - d1).days
    print(dt)
    print(d1.isoweekday())  # 6
    print(dt // 7 + 1)  # 40

  3.time类
  
    class time:
        def __init__(self, hour, minute, second, microsecond, tzinfo):
            pass

    如何使用 datetime.time() 类？

    import datetime

    t = datetime.time(12, 9, 23, 12980)
    print(t)  # 12:09:23.012980
    print(type(t))  # <class 'datetime.time'>
    注意：

    1秒 = 1000 毫秒（milliseconds）
    1毫秒 = 1000 微妙（microseconds）

    如何将给定日期转换为当天开始的时间？

    # 输入
    import datetime
    date = datetime.date(2019, 10, 2)

    # 输出
    2019-10-02 00:00:00

    import datetime

    date = datetime.date(2019, 10, 2)
    dt = datetime.datetime(date.year, date.month, date.day)
    print(dt)  # 2019-10-02 00:00:00

    dt = datetime.datetime.combine(date, datetime.time.min)
    print(dt)  # 2019-10-02 00:00:00

4.timedelta类

    timedelta 表示具体时间实例中的一段时间。你可以把它们简单想象成两个日期或时间之间的间隔。

    它常常被用来从 datetime 对象中添加或移除一段特定的时间。

    class timedelta(SupportsAbs[timedelta]):
        def __init__(self, days, seconds, microseconds, milliseconds, minutes, hours, weeks,):
            pass
        def days(self):
            pass
        def total_seconds(self):
            pass

    如何使用 datetime.timedelta() 类？

    import datetime

    td = datetime.timedelta(days=30)
    print(td)  # 30 days, 0:00:00
    print(type(td))  # <class 'datetime.timedelta'>
    print(datetime.date.today())  # 2020-07-01
    print(datetime.date.today() + td)  # 2020-07-31


    如果将两个 datetime 对象相减，就会得到表示该时间间隔的 timedelta 对象。

    同样地，将两个时间间隔相减，可以得到另一个 timedelta 对象。



    距离你出生那天过去多少天了？
    距离你今年的下一个生日还有多少天？
    将距离你今年的下一个生日的天数转换为秒数。
    # 输入
    bday = 'Oct 2, 1969'


    from dateutil import parser
    import datetime

    bDay = 'Oct 2, 1969'
    dt1 = parser.parse(bDay).date()
    dt2 = datetime.date.today()
    dt3 = datetime.date(dt2.year, dt1.month, dt1.day)
    print(dt1)  # 1969-10-02
    print(dt2)  # 2020-07-01
    print(dt3)  # 2020-10-02

    td = dt2 - dt1
    print(td.days)  # 18535
    td = dt3 - dt2
    print(td.days)  # 93
    print(td.days * 24 * 60 * 60)  # 8035200
    print(td.total_seconds())  # 8035200.0

练习题：

    1、假设你获取了用户输入的日期和时间如2020-1-21 9:01:30，以及一个时区信息如UTC+5:00，均是str，请编写一个函数将其转换为timestamp：

    题目说明:

    """

    Input file
    example1: dt_str='2020-6-1 08:10:30', tz_str='UTC+7:00'
    example2: dt_str='2020-5-31 16:10:30', tz_str='UTC-09:00'

    Output file
    result1: 1590973830.0
    result2: 1590973830.0
    """


    def to_timestamp(dt_str, tz_str):
        # your code here
            pass

        import datetime
        from dateutil import tz, zoneinfo

        def to_timestamp(dt_str, tz_str):
          [year, month, day] = [int(i) for i in dt_str.split(' ')[0].split('-')]
          [hour,mint, sec] = [int(i) for i in dt_str.split(' ')[1].split(':')]
          t = datetime.datetime(year=year, month=month, day=day, hour=hour, minute=mint, second=sec, tzinfo = tz.gettz(tz_str))
          return t.timestamp()

    In [32]: dt_str='2020-6-1 08:10:30'
        ...: tz_str='UTC+7:00'
        ...: to_timestamp(dt_str, tz_str)
    Out[32]: 1590973830.0

    In [33]: dt_str='2020-5-31 16:10:30'
        ...: tz_str='UTC-09:00'
        ...: to_timestamp(dt_str, tz_str)
    Out[33]: 1590973830.0       

    2、编写Python程序以选择指定年份的所有星期日。

    题目说明:



    def all_sundays(year):
        # your code here
        """

    Input file
       2020

    Output file
       2020-01-05                         
       2020-01-12              
       2020-01-19                
       2020-01-26               
       2020-02-02     
       -----
       2020-12-06               
       2020-12-13                
       2020-12-20                
       2020-12-27 
    """
    import datetime

    def all_sundays(year):

      init_date = datetime.date(int(year),1,1)
      w1 = init_date.isoweekday()
      delta_day = 7 - w1
      first7 = init_date  + datetime.timedelta(days = delta_day)
        while first7.year<year+1:
          print(first7)
          first7 = first7 + datetime.timedelta(days = 7)

    In [44]: all_sundays(2020)
    2020-01-05
    2020-01-12
    2020-01-19
    2020-01-26
    2020-02-02
    2020-02-09
    2020-02-16
    2020-02-23
    2020-03-01
    2020-03-08
    2020-03-15
    2020-03-22
    2020-03-29
    2020-04-05
    2020-04-12
    2020-04-19
    2020-04-26
    2020-05-03
    2020-05-10
    2020-05-17
    2020-05-24
    2020-05-31
    2020-06-07
    2020-06-14
    2020-06-21
    2020-06-28
    2020-07-05
    2020-07-12
    2020-07-19
    2020-07-26
    2020-08-02
    2020-08-09
    2020-08-16
    2020-08-23
    2020-08-30
    2020-09-06
    2020-09-13
    2020-09-20
    2020-09-27
    2020-10-04
    2020-10-11
    2020-10-18
    2020-10-25
    2020-11-01
    2020-11-08
    2020-11-15
    2020-11-22
    2020-11-29
    2020-12-06
    2020-12-13
    2020-12-20
    2020-12-27

    

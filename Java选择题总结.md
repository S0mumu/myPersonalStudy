#JAVA选择题总结
------
###构造器
	1. 构造器没有返回值，这个跟void可不等同
	2. 每一个类若没有显式声明一个构建器，则会有一个默认的无参构建器
	3. 构建器可以重载，可以通过super()、this()相互调用
	4. 每一个构造器默认第一行都是super()，但是父类中若是没有无参构造器，则子类必须显式调用父类中的构造器
###抽象类 && 接口
	1. abstract class 类名{
			...
	 	}
	2. 抽象方法中不能有方法体
	3. 在jdk1.8中，抽象类可以有构造方法，接口中没有构造方法，不能实例化接口对象
	4. 在jdk1.8中，接口可以default、static方法。接口的方法默认是abstract，成员变量默认是static final
	5. 在jdk1.8之前接口都只能有抽象方法，因此当一个接口被多个类实现时，如果在实际的工程中，需要在借口中添加抽象方法，且其对应的实现类都需要用到的话，则代码的维护就不够灵活，因此jdk1.8中在接口中新增一个default方法，这个默认方法有具体方法的实现，就可以不用去修改实体类了。
###java concurrent包中的类
	1. Semaphore: 控制某个资源可以被同时访问的个数，就像是一个数据库连接池。
	2. ReentrantLock: 与使用synchronized方法和语句所访问的隐式监视器锁相同的基本行为和语义，用于锁定线程，但是它的功能更强
	3. Future: 异步计算的结果，它是一个接口，只用于获取线程结果
	4. CountDownLatch: 在一个线程中等待多个线程完成，是一个锁存器，他表示我要占用给定的多个线程且优先执行，在其执行完之前，其他需要该资源的都需要等待
###try catch语句
	1. try中抛出异常，且被catch捕获则try后面的语句不执行，执行catch中的语句，且可以执行try catch finally外部的语句。
###java语言的标识符
	1. 不能是java中的关键字、保留字
	2. 字母、数字、下划线、$
	3. 首字母不能是数字
###后台线程 && 前台线程
	1. 后台线程为其他线程提供服务，也称为守护线程，例如jvm的垃圾回收线程就是一个后台线程
	2. 前台线程，例如main函数是一个前台线程，在程序中必须执行完成，是jre判断程序是否执行结束的标志
###servlet过滤器
	1.使用时，需要在web.xml中进行配置
		 <filter> 包括<filter-name> <filter-class>
		<filter-mappping> 可以映射到一个或多个servlet或jsp文件，也可以采用<url-pattern>映射到任意的url
###switch
	1. java7之前，switch后只能支持byte、short、char、int或者其对应的包装类，以及Enum类型。在java7时支持String。switch后不能使用float、double、boolean。
	2. switch表达式的值不能为null，在运行时会抛出NullPointerException。
	3. case子句也不能使用null，会出现编译错误。
	4. 字符串中可以包含转义字符，例如“男”和“\u7537”是等同的。
###饿汉式单例模式
	class Chinese{
		private static Chinese obj=new Chinese();
		private Chinese(){
		
		}
		public static Chinese getInstance(){
			return obj;
		}
	}
	
	public class TestChinese{
		public static void main(String[] args){
			Chinese obj1=Chinese.getInstance();
			Chinese obj2=Chinese.getInstance();
			System.out.println(obj1==obj2);//true
		}
	}
	
	单例模式实现的步骤：
	1. 构造器私有化，外部类无法构造创建对象。
	2. 本类提供一个static方法【由于没有对象调用，这个方法为类方法，通过类名直接调用】，外部类通过调用这个方法获得唯一的对象。
	3. 由于类方法只能调用本类的静态对象，因此设置对象变量为static，类变量。
	4. 类变量和类方法在类加载时初始化，只加载一次。
###Collection接口和Map接口
	1. Collection接口：
			List接口
				LinkedList 非同步
				ArrayList 非同步，实现了可变大小的元素数组
				Vector 同步
					Stack
	2. Set接口
	3.	Map接口
			Hashtable 同步，实现一个key-value的映射
			HashMap 非同步
			WeakHashMap 改进HashMap，实现“弱引用”，如果一个key没有被引用，则会被GC回收（垃圾回收）
###局部变量（方法变量） && 成员变量（类成员）
	1. 局部变量没有默认值，在未赋值前使用编译器报错。
	2. 成员变量有默认值
###类型运算
	1. java中的byte，short，char进行运算的时候会自动提升为int类型。
		byte b1=9,b2=10,b3;
		b3=b1+b2;//错误
###线程yield方法
	1. Thread.yield()方法，暂停当前正在执行的线程对象，并执行其他线程，将当前线程转为可运行状态，以允许相同优先级的进程获得运行机会，但无法保证达到让步机会，因为yield线程仍有可能被选中执行。
###代码优化
	1. 代码优化可以分为局部优化、循环优化和全局优化
		局部优化：指的是在只有一个入口、一个出口的基本程序块上进行的优化。
		循环优化：是对代码中的循环代码块进行优化；代码外提、强度削弱、删除归纳变量
		全局优化：整个程序范围内优化
		
		删除多余运算：删除公共子表达式
###程序名称
	1. 如果有公共类（public）的话，则要求源文件名和外部公共类名一样，如果没有公共类的话，则不要求。
	2. 在编写一个Java源文件（编译单元）的时候，在编译单元的内部只可以有一个public类，该类的名称必须与文件的名称相同。
	3. 方便虚拟机在相应的路径中找到相应类所对应的字节码文件
###transient变量
	1. 这个变量和序列化有关，该变量标识的对象不可以被序列化，具体的序列化有ObjectInputStream和ObjectOutputStream完成，static修饰的变量不可序列化。
###Maven&&Ant
	1. Maven和Ant都是Java的构建工具。Ant是软件构建工具，Maven是项目管理、理解工具。
	2. Ant没有一个约定的目录结构，没有生命周期，必要定义目标及其实现的任务序列，没有集成依赖。
	3. Maven有约定的目录结构，有生命周期，mvn install就可以自动编译、测试、打包，定义有pom.xml依赖管理、仓库管理。
###静态变量
	1. 只可以在类中定义，不可以在方法中定义。
	2. 不可被序列化。
###Math包
	1. Math.cos计算弧度的余弦值，Math.toRadians角度转弧度，Math.toDegrees弧度转角度。
###线程安全的数据结构
	1. 喂！SHE！
	2. vector stack hashtable enumeration
###重载
	1.函数名相同，无关返回值【可相同可不同】，参数不同
###构造器
	1. 构造方法优先级比一般方法低。
		静态成员变量或静态代码块>main方法>非静态成员变量或非静态代码块>构造方法
	2. 构造器没有返回值
	3. 对类对象进行初始化
	4. 在new对象时，自动调用构造方法

![avatar](kkk.png)
	
	
	
	
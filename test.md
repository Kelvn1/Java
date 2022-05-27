#+ 最终代码
	匹萨父类：
	package com.msb.test01;
	/**
	* @Auther: msb-zhaoss
	* 父类：匹萨类
	*/
	public class Pizza {
	//属性
	private String name;//名称
	private int size;//大小
	private int price;//价格
	//方法
	public String getName() {
	return name;
	}
	public void setName(String name) {
	this.name = name;
	}
	public int getSize() {
	return size;
	}
	public void setSize(int size) {
	this.size = size;
	}
	public int getPrice() {
	return price;
	}
	public void setPrice(int price) {
	this.price = price;
	}
	//展示匹萨信息：
	public String showPizza(){
	return "匹萨的名字是："+name+"\n匹萨的大小是："+size+"寸\n匹萨的价格："+price+"元";
	}
	//构造器
	public Pizza() {
	}
	public Pizza(String name, int size, int price) {
	this.name = name;
	this.size = size;
	this.price = price;
	}
	}
	培根匹萨：
	package com.msb.test01;
	/**
	* @Auther: msb-zhaoss
	*/
	public class BaconPizza extends Pizza {
	//属性：
	private int weight;
	public int getWeight() {
	return weight;
	}
	public void setWeight(int weight) {
	this.weight = weight;
	}
	//构造器：
	public BaconPizza() {
	}
	public BaconPizza(String name, int size, int price, int weight) {
	super(name, size, price);
	this.weight = weight;
	}
	//重写父类showPizza方法：
	@Override
	public String showPizza() {
	return super.showPizza()+"\n培根的克数是："+weight+"克";
	}
	}
	水果匹萨：
	package com.msb.test01;
	/**
	* @Auther: msb-zhaoss
	*/
	public class FruitsPizza extends Pizza{
	//属性：
	private String burdening;
	public String getBurdening() {
	return burdening;
	}
	public void setBurdening(String burdening) {
	this.burdening = burdening;
	}
	//构造器：
	public FruitsPizza() {
	}
	public FruitsPizza(String name, int size, int price, String burdening) {
	super(name, size, price);
	this.burdening = burdening;
	}
	//重写父类showPizza方法：
	@Override
	public String showPizza() {
	return super.showPizza()+"\n你要加入的水果："+burdening;
	}
	}
	测试类：
	public class Test {
	//入口方法main
	public static void main(String[] args) {
	//Test类，实例化一个对象，调用相应方法
	Test t = new Test();
	t.menuLoop();//选择菜单
	}
	//循环显示购买菜单
	private void menuLoop(){
	menu();
	}
	//主菜单
	private void menu() {
	//选择购买的披萨
	//利用java自带类，定义输入
	Scanner sc = new Scanner(System.in);
	System.out.println("*********蛋 糕 选 择*********");
	System.out.println("\t 1.培根披萨\t 2.水果披萨\t 3.退出");
	System.out.print("请输入选项对应的数字：");
	int choice = sc.nextInt();//选择披萨类型
	if (choice == 3) {
	System.exit(0);
	} else {
	//通过工厂获取披萨：
	Pizza pizza = PizzaStore.getPizza(choice);//接收的是以父类为返回值的，接收后，向下转型
	System.out.println(pizza.showPizza());
	System.out.println("------------选择完毕，可以在下面继续选择------------");
	menu();
	}
	}
	}
	工厂类：
	import java.util.Scanner;
	//单独设计的披萨工厂，通过 多态 特性，对不同披萨进行处理
	public class PizzaStore {
	//父类作为方法返回值，根据传入参数，产生具体类型
	public static Pizza getPizza(int choice){
	Scanner sc = new Scanner(System.in);
	Pizza p = null;
	switch (choice){
	case 1:{
	System.out.println("^^^^^^^^^^^披萨类型的选择^^^^^^^^^^^");
	System.out.print("请录入培根的克数：");
	int weight = sc.nextInt();
	System.out.println();
	System.out.print("请录入匹萨的大小：");
	int size = sc.nextInt();
	System.out.println();
	System.out.print("请录入匹萨的价格：");
	int price = sc.nextInt();
	System.out.println();
	//根据录入信息，封装为培根的对象：
	BaconPizza bp = new BaconPizza("培根披萨",size,price,weight);
	p = bp;//多态， 将创建的培根披萨的内存空间地址赋给 父类对象 p
	} break;
	case 2:{
	System.out.println("^^^^^^^^^^^披萨类型的选择^^^^^^^^^^^");
	System.out.print("请录入你想要加入的水果：");
	String burdening = sc.next();
	System.out.println();
	System.out.print("请录入匹萨的大小：");
	int size = sc.nextInt();
	System.out.println();
	System.out.print("请录入匹萨的价格：");
	int price = sc.nextInt();
	System.out.println();
	//根据录入信息，封装为水果披萨的对象：
	FruitsPizza fp = new FruitsPizza("水果披萨",size,price,burdening);
	p = fp;//多态， 将创建的培根披萨的内存空间地址赋给 父类对象 p
	} break;
	}
	return p;
	}
	}

#Python学习手册－函数

## 函数的参数  

1. 位置参数  

	最基本的参数，顾名思义，就是基于位置的参数，必不可少，如果调用函数时缺少传入位置参数，则会报错。举例如下：  
	
		def power(x,n):
			s=1
			while n>0
				n=n-1
				s=s*x
			return s
	在这里面，x和n就是位置参数
2. 默认参数
	
	默认参数是在定义函数时，我们将某一参数给予一个默认值，这样当调用函数时，我们可以缺省传入这一参数，函数会自动使用在定义时的默认值。因此这种参数叫做默认参数，这可不是默认必须有的意思，而是可以没有的参数：
		
		def power(x,n＝2):
			s=1
			while n>0
				n=n-1
				s=s*x
			return s
	这里的n就是默认参数，默认值是2.当我们调用power函数时，可以不传入n的值，函数会默认n＝2.
	
	默认参数的好处是降低了函数调用的难度，比较通用，有需要可以传入，不需要则不传入。
	
	特别注意，默认参数必须指向**不变对象** (str/None,而不是dict／tuple)
3. 可变参数

	故名思意，指传入的参数**个数**是可变的
			
		def calc(*numbers):
			sum=0
			for n in numbers:
				sum=sum+n*n
			return sum
	这里的*numbers就是一个可变参数，调用函数时，可以`calc(1,2,3)`,函数会自动把1，2，3组合成一个`tuple＝（1，2，3）`当然调用时也可以给函数传入一个tuple，如下：
	
		nums=[1,2,3]
		calc(*num)
	只要在给函数传参时在前面加一个星号`*`即可
4. 关键字参数
	
	类似可变参数，可变参数时将传入的参数组成一个tuple，而关键词参数是将传入的参数组成一个dict：
		
		def person(name,age,**kw):
			print('name:',name,'age:',age,'other:',kw)
	这里只有name和age是位置参数（必选），kw就是关键字参数。
5. 命名关键字参数

	上一趴关键字参数可以传入不受限制的内容，那么命名关键字参数，就是关键字参数中必须传入符合函数定义是的命名，如下：
		
		def person(name,age,*,city,job):
			print(name,age,city,job)
	
	＊是用来区分位置参数和命名关键字参数的分隔符，必须有。
	在调用时，必须传入city和job两个关键字参数名。如下是不可以的：
	
		person('Jack',24,'Beijing','Engineer')
	由于缺乏参数名，Python解释器会把这4个参数都视为位置参数，但`person()`这个函数只有2个位置参数。这样就会报错了。
	当然，命名关键字参数也可以使用默认值，这样在调用时，可以不传入有默认值的参数：
		
		def person(name,age,*,city='Beijing',job):
			print(name,age,city,job)

6. 参数组合

	顾名思义，即将以上5种参数在一个函数中混合使用，但参数定义的顺序必须是：
	
	a. 必选参数
	b. 默认参数
	c. 可变参数
	d. 命名关键字参数
	f. 关键字参数

## 递归函数
如果一个函数在内部调用本身，那就是一个递归函数。
为了防止栈溢出，我们可以使用 *尾递归优化* ：在函数返回时，调用自身本身，并且，return语句不能包含表达式。
		
	def fact(n):
		return fact_iter(n,1)
	
	def fact_iter(num,product):
		if num==1:
			return product
		return fact_iter(num-1,num*product)
	 
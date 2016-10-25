#### ��Сջ��ʵ��

#### ѧ��Java�Ķ�֪����һ�����ݽṹ��ջ�����ǰ��������Ƚ������ԭ�������ݣ�����Stack��������͵�һ���ࣻ

#### һ��ջ�Ļ������


> ջ��һ�����ݽṹ��ֻ����ĳһ�˲����ɾ�����������Ա���������������ԭ�������ݡ������Ƚ�������ݱ�ѹ�ŵ�ջ�ף���������ݱ���ŵ�ջ�����������Ҫ��ȡ����Ҫ�ӵ�һ��ջ����ʼ��ȡ����һ�����ݱ����һ�ζ�ȡ����

> ջ������ͬһ�˽��в����ɾ���������������Ա�������в����ɾ����һ�˳�֮Ϊջ��������һ�˳�Ϊջ�ף�ջ�׹̶�����ջ���Ǹ����ġ�


![stack](https://github.com/gifmeryshuai/markDown-ImageCahce/blob/master/stack.png?raw=true)


#### ����ջ��ʹ�÷���

>     �˽���ջ�ĸ���֮���������ڿ�һ�¾���ջ�����Ĵ��룺
```xml
public static void stackTest() {
		
		/**
		 * ����ջ��ʵ��
		 * Stack<Object> ����ʹ�÷���
		 */
		Stack stack = new Stack();
		/**
		 * ��ջʹ��push����
		 * push(Object)������Object���ͣ���������������κζ���
		 * 
		 */
		stack.push(123);
		printMsg(stack);
		
		stack.push("MSG");
		printMsg(stack);
		
		stack.push(789);
		printMsg(stack);
		
		stack.push("XYZ");
		printMsg(stack);
		
		stack.push(3.14);
		
		stack.push('d');
		printMsg(stack);
		
		/**
		 * ĿǰΪֹ'd'Ϊջ��
		 * ����ִ��pop����֮��
		 * XYZ�ͳ���ջ����
		 */
		stack.pop();
		printMsg(stack);
		
		System.out
				.println("peek:" + stack.peek() + ",elementAt:" + stack.elementAt(0) + ",search:" + stack.search("XYZ")
						+ ",firstElement:" + stack.firstElement() + ",lastElement:" + stack.lastElement());
	}
	
	public static void printMsg(Stack stack) {
		
		//empty �ж� ��Stack�Ƿ�Ϊ�գ�Ҳ����ջ���Ƿ�û���ˣ�
		if(stack != null && !stack.empty()) {
			//ͨ��Enumerationö���г�����Ԫ��
			Enumeration enumeration = stack.elements();
			
			System.out.println("StackԪ������");
			
			//ѭ����������ö�ٵ�Ԫ��
			while(enumeration.hasMoreElements()) {
				System.out.print(enumeration.nextElement()+"  ");
			}
			System.out.println("");
		}
	}


//��ӡ���

		/**
		 *
		 * StackԪ������
         * 123  
         * StackԪ������
         * 123  MSG  
         * StackԪ������
         * 123  MSG  789  
         * StackԪ������
         * 123  MSG  789  XYZ  
         * StackԪ������
         * 123  MSG  789  XYZ  3.14  d  
         * StackԪ������
         * 123  MSG  789  XYZ  3.14  
         * ��ȡջ��Ԫ��peek:3.14,
         * ����ջ��������ȡԪ��elementAt:123,
         * ����Ԫ�ػ�ȡջ�е�����search:2,
         * ��ȡջ��Ԫ��firstElement:123,
         * ��ȡջ��Ԫ��lastElement:3.14
         * 
		 **/
```



#### ������Сջ��ʵ��
> �����Ѿ�˵�ˣ�ջ�Ļ���ʹ�÷�����������������ôһ�����⣻



```
�����һ��ջ��Ҫ�г�ջ��pop��,��ջ(push)�����л�ȡ��Сֵ��getMin������;

˼·��

1. ��������һ�����ͱ���int min����ʼֵΪ-1��
2. ����һ��Ԫ����ջ��ʱ�򣬽�minֵ��ֵΪ0��
3. ֮��ÿ����Ԫ����ջ��ʱ�򣬶�Ҫ��min������ָ����ջ�����ݽ��бȽϣ����С����Ԫ����ô������min��ֵΪ��Ԫ�ص�����������ά��min��ֵ���䣻
4. ������getMin�ķ���ʱ�򣬾�ͨ��stack.elementAt(min)����ȡ������
```
![image](https://github.com/gifmeryshuai/markDown-ImageCahce/blob/master/stack-1.png?raw=true)
![image](https://github.com/gifmeryshuai/markDown-ImageCahce/blob/master/stack-2.png?raw=true)
![image](https://github.com/gifmeryshuai/markDown-ImageCahce/blob/master/stack-3.png?raw=true)

> ֪��˼·֮�����ǿ����룺����Ҫ����ȡջ����Сֵ�ķ�����
```xml
/**
	 * ����һ
	 */
	public static void method1() {

		int min = -1;

//		// ����ջ
		Stack<Integer> stack = new Stack<Integer>();
//
//		// ����һ��Ԫ�ؾ���ջ�о�Ĭ�ϼ�¼��ֵ��ջ����С��һ��Ԫ��
//		stack.push(new Integer(10));
//		// ��min��Ϊ0��������СԪ�ص�����
//		min = 0;
//
//		// �ڶ���Ԫ�������СԪ�صıȽϣ�������ھ͸ı�min���ݣ���֮��¼�½���Ԫ�ص�����λ�ã�
//		stack.push(new Integer(12));
//		if (stack.get(min) > (new Integer(12))) {
//
//			min = 1;
//		}
//
//		stack.push(new Integer(9));
//		if (stack.get(min) > (new Integer(9))) {
//
//			min = 2;
//		}
//		stack.push(new Integer(4));
//		if (stack.get(min) > (new Integer(4))) {
//
//			min = 3;
//		}
//		stack.push(new Integer(7));
//		if (stack.get(min) > (new Integer(7))) {
//
//			min = 4;
//		}
//
//		printStack(stack);
//		
//		
//		System.out.println("��Сֵ��"+stack.get(min)+", ������"+min);
		
		
		Integer[] integers = new Integer[]{9, 1, 4, 8, 3};
		
		for(int i = 0 ; i < integers.length ; i++) {
			
			stack.push(integers[i]);
			if(i == 0) {

				min = 0;
			}else {
				
				if(stack.get(min) >= integers[i]) {
					
					min = i;
				}
			}
			
			
		}
		printStack(stack);
		
		
		System.out.println("��Сֵ��"+stack.get(min)+", ������"+min);
		
		//����Stack��Сֵ��ջ��������ִ��pop��ȥջ���������Ǿ��Ҳ�����Сֵ��
		//��������Ҫ�����ջ�׵�ջ�������е���С���ݵ�����
	}

	public static void printStack(Stack<Integer> stack) {

		if (stack != null) {

			if (stack.empty()) {
				System.out.println("ջΪ��");
			} else {

				Enumeration item = stack.elements();// ��ȡstack��ö�ٶ���

				System.out.print("��ջ�е�Ԫ�أ�");
				while (item.hasMoreElements()) {
					System.out.print(item.nextElement() + " ");// ����ö�������е�Ԫ��
				}
				System.out.println();
			}
		}
	}
	/**
	 * ��ջ�е�Ԫ�أ�9 10 4 8 3
     * ��Сֵ��3, ������4
	 */
```
> ĿǰΪֹ�������Ѿ���ȡ����ջ�еĵ���С��Ԫ�أ��Լ�������λ�á����ǣ����ջ�����pop�Ƴ���ջһ��Ԫ�أ������ջ����Ԫ����������С��Ԫ�ظ���ô�죿����ȷ������ջ�еġ�3��������ջ����Ԫ�أ�������Ҳ��ջ����С��Ԫ�أ���ôpop()֮�����Ǿ��Ҳ�����ջ����С��Ԫ���ˣ�min�����¼��ֵҲ�ͳ���ջ�г��������ˣ�Ҳ����˵û�б�̥�ˣ�û�������������������ˣ��������������������ģ�
---

```
˼·��
1.  ���ȴ���һ���洢����Ԫ�ص�stack-Aջ��֮���ڴ���һ������Aջ��СԪ�ص�����
2.  ����һ��Ԫ�ؽ���A-ջ��ʱ��B-ջ��Ĭ�ϱ���A-ջ�е�һ��ջ��Ԫ������Ҳ����A-ջ��ջ�ף�
3.  ÿһ�����µ�Ԫ�ؽ���A-ջ��Ҫ��B-ջ��ջ����ȡ����ֵ����A-ջͨ�������õ�Ԫ��ֵ����Ԫ�ؽ��бȽϣ������Ԫ��С��A-ջ����СԪ�صĻ�����ô�ͽ������Ԫ�ص���������B-ջ��
4.  ���A-ջ���Ƴ�ջ��Ԫ�أ�����Ҫ��B-ջ��ջ��Ԫ�ػ�ȡ������A-ջ�õ���������Ԫ�أ��жϴ�Ԫ���Ƿ���ջ��Ԫ�أ�����ǣ���ô�ͽ�B-ջ�е�ջ��Ԫ��Ҳ��Ӧ���Ƴ����������������Ҫ��ȡA-ջ����СԪ�أ�ֱ�ӾͿ��Դ�B-ջ��ջ���ڵõ�Ԫ��ֵ����A-ջ���ɣ�
5. ͬ����ȡgetMin��СԪ��ֵ��Ҳ��һ������B-ջ�еõ�ջ��Ԫ�أ�����A-ջ���õ���СԪ�أ�
```

```xml
public static void method2() {
		
		/**
		 * �洢Ԫ��stack
		 */
		Stack<Integer> stack_A = new Stack<Integer>();
		/**
		 * �洢stack_A����СԪ�ص�����
		 */
		Stack<Integer> stack_B = new Stack<Integer>();
		
		Integer[] integers = new Integer[]{9, 18, 2, 7, 29, 3, 6, 2, 8, 13, 4};
		
		for(int i = 0 ; i < integers.length ; i++) {
			
			int value = integers[i];
			pushStack_A(stack_A, stack_B, value);
			
			//��ջ
//			stack_A.push(integers[i]);
//			if(i == 0) {
//
//				//��һ��Ĭ�ϱ�����ջ��Ԫ������
//				stack_B.push(i);
//			}else {
//				//��ȡstack_Bջ��Ԫ�أ�����stack_A��stack_A��ȡ��Сֵ����Ԫ�ؽ��бȽ�
//				//���������Ԫ��˵������Ԫ������Сֵ��
//				if(stack_A.get(stack_B.lastElement()) >= stack_A.lastElement()) {
//					//֮�󱣴���Ԫ�ص�����ֵ��stack_B�У�
//					stack_B.push(i);
//				}
//			}
		}
		System.out.println("stack_A����Ԫ�أ�");
		printStack(stack_A);
		System.out.println("stack_B����Ԫ�أ�");
		printStack(stack_B);
		
		for(int i = 0 ; i <6;i++) {
			popStack_A(stack_A, stack_B);
			
		}
		
//		System.out.println(""+stack_A.size());
//		System.out.println("��ȥStack_Aջ��:"+stack_A.pop());
//		System.out.println(""+stack_A.size());
//		System.out.println("��ȥStack_B�Ķ�Ӧ������:"+stack_B.pop());
		
		
		System.out.println("stack_A����Ԫ�أ�");
		printStack(stack_A);
		System.out.println("stack_B����Ԫ�أ�");
		
		printStack(stack_B);
	}
	
	
	
```
#### Stack_A�Ƴ�Ԫ��
```xml
	public static void popStack_A(Stack<Integer> stack_A, Stack<Integer> stack_B) {
		
		System.out.println("�Ƴ�Stack_AԪ��:"+stack_A.pop());
		if(stack_A.size() == stack_B.lastElement()) {
			
			System.out.println("�Ƴ�Stack_Bջ��:"+stack_B.pop());
		}
		
	}
```
#### Stack_A��push����
```xml
	public static void pushStack_A(Stack<Integer> stack_A, Stack<Integer> stack_B, int value) {
		//��һ��Ĭ�ϱ�����ջ��Ԫ������
		if(stack_A.size() == 0) {
			
			stack_A.push(value);
			stack_B.clear();
			stack_B.push(0);
		}else {
			//��ȡstack_Bջ��Ԫ�أ�����stack_A��stack_A��ȡ��Сֵ����Ԫ�ؽ��бȽ�
//			//���������Ԫ��˵������Ԫ������Сֵ��
			stack_A.push(value);
			if(stack_A.elementAt(stack_B.lastElement()) >= stack_A.lastElement()) {
				//֮�󱣴���Ԫ�ص�����ֵ��stack_B�У�
				stack_B.push(stack_A.size()-1);
			}
		}
		
	}
```


---

```
����Ĵ����Ѿ������棻
����һ�����⣬���������Ҫͨ��Java������һ����ʽ�Ľṹ���൱��LinkList����ʵ�ָ���ôʵ�֣�
```

```xml

package com.test.node;

public class MinStacks {

	public static void main(String [] args) {
		
		MinStacks stacks = new MinStacks();
		stacks.pushStack(10);
		stacks.pushStack(12);
		stacks.pushStack(5);
		stacks.pushStack(13);
		stacks.pushStack(0);
		stacks.pushStack(2);
		stacks.pushStack(34);
		
		System.out.println("ԭʼԪ��:");
		stacks.printStack();
		
		System.out.println("�Ƴ�Ԫ��:"+stacks.popStack());
		System.out.println("�Ƴ�Ԫ��:"+stacks.popStack());
		System.out.println("�Ƴ�Ԫ��:"+stacks.popStack());
		
		System.out.println("��Сֵ:"+stacks.getMin());
		System.out.println("����Ԫ��:");
		System.out.print(stacks.top.value+", ");
		Nodes nodes = stacks.top.node;
		while(nodes!= null) {
			
			System.out.print(nodes.value+", ");
			nodes = nodes.node;
		}
	}
	private Nodes top;
	public int popStack() {
		int result = 0;
		//�����ͷ��Ϊ��˵�����ٻ���һ��Nodes�ڵ�
		if(top != null) {
			//�õ�Nodes��valueֵ��Ҳ����ջ��Ԫ��ֵ
			result = top.value;
			//��ȡ��ͷ��Nodes����һ��Nodes
			Nodes nodes = top.node;
			//����һ��Nodes�ڵ���Ϊ��
			top.node = null;
			//����һ��Nodes�Ľڵ㱻top�ڵ����õ�ǰ��ͷ�ڵ�
			top = nodes; 
			
			return result;
		}
		
		return result;
	}
	
	
	public void pushStack(int value) {
		
		if(top == null) {
			//�״�ִ�У���Nodes�ڵ��һ����ʱ��min��valueĬ������Сֵ
			top = new Nodes(value, value);
		}else {
			
			//�����Ԫ����ӽ���������һ��Ԫ�غ���Ԫ��value�Ƚϣ��õ���Сֵ��������Ԫ�ؽڵ���
			Nodes nodes = new Nodes(value, Math.min(value, top.min));

			/**
			 * ͨ����������
			 * ����һ���ڵ�����Ԫ���ڲ���Nodes����
			 * ����Ԫ����top����
			 * ��ʵҲ���ǽ���Ԫ�ط�������ı�ͷ��
			 */
			nodes.node = top;
			top = nodes;
		}
	}
	
	public int getMin() {
		
		int min = top.min;
		
		int index  = 0;
		
		Nodes nodes = top;
		
		while(nodes !=  null) {
			
			if(nodes.value == min) 
				break;
			
			nodes = nodes.node;
			index++;
		}
		System.out.println("λ��:"+index);
		
		return min;
	}
	
	/*
	 * ��ӡ���нڵ�value��ֵ
	 */
	private void printStack() {
		
		Nodes nodes = top;

		/**
		 * ͨ��ѭ���õ�
		 */
		while(nodes != null) {
			
			System.out.print(nodes.value+", ");
			nodes = nodes.node;
		}
		System.out.println();
	}
	

}


```


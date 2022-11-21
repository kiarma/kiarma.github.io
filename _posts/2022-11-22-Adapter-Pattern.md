---
layout: post
title:  ���ģʽ������
category: ���ģʽ
---

# ����������������ģʽ | Spring �е�������

![���������ģʽ](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjtnx5644j30hs0b4mxx.jpg)



## ����

������������һ�׹�Ʊ����ϵͳ�������ṩ���������ṩ XML ��ʽ���ݣ����ǻ�ȡ����������ʾ������ϵͳ�ĵ���������Ҫ����һЩ������ϵͳ�Ķ������ݣ���������ֻ�ṩ��ȡ JSON ��ʽ�����ݽӿڡ�

�ڲ���ı�ԭ�д����߼�������£���ν���أ�

��ʱ�����ǾͿ��Դ���һ����**������**��������һ������Ķ��� �ܹ�ת������ӿڣ� ʹ����������������н�����

������ģʽͨ����װ���󽫸��ӵ�ת������������Ļ�� ����װ�Ķ���������������������Ĵ��ڡ� 

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjt8avun0j31py0kztda.jpg)



## ��ʵ�������

��������ʲô��������⣬������Ҳ�洦�ɼ������磬�ʼǱ����Եĵ�Դ�����������ܳ䣨������������һ����ôţ�Ƶ����֣���һ��ʮ�����ߵȵȡ�

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjhf9tjluj32hc0mu4p8.jpg)



## ��������

- ������ģʽ��һ����Ľӿڣ�ת���ɿͻ�����������һ���ӿڡ���������ԭ���ӿڲ����ݵ�����Ժ����޼䡣Ҳ���Խа�װ����Wrapper��

- **������ģʽ**��һ�ֽṹ�����ģʽ�� ����ʹ�ӿڲ����ݵĶ����ܹ��໥����
- ��Ҫ��Ϊ���ࣺ��������ģʽ������������ģʽ



## ����ԭ��

- ������ģʽ����һ����Ľӿ�ת������һ�ֽӿڣ���ԭ���ӿڲ����ݵ�����Լ���
- ���û��ĽǶȿ������������ߣ��ǽ����
- �û�����������ת��������Ŀ��ӿڷ������������ٵ��ñ������ߵ���ؽӿڷ���
- �û��յ�����������о�ֻ�Ǻ�Ŀ��ӿڽ���



## ������ģʽ�ṹ

### ����������

ʵ��ʱʹ���˹���ԭ�� ������ʵ��������һ������Ľӿڣ� ������һ��������з�װ�� �������еı�����Զ�����ʵ����������

![���������ģʽ�Ľṹ��������������](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjjbh88h7j31od0u0ds2.jpg)

1. **�ͻ���** ��Client�� �ǰ�����ǰ����ҵ���߼����ࡣ
2. **�ͻ��˽ӿ�** ��Target�� ��������������ͻ��˴������ʱ������ѭ��Э�顣
3. **����** ��Service�� ����һЩ������ ��ͨ�����Ե�����������ϵͳ���� �ͻ�������ӿڲ����ݣ� ����޷�ֱ�ӵ����书�ܣ�Ҳ���Խ��������ࣨAdaptee����
4. **������** ��Adapter�� ��һ������ͬʱ��ͻ��˺ͷ��񽻻����ࣺ ����ʵ�ֿͻ��˽ӿڵ�ͬʱ��װ�˷������ ���������ܿͻ���ͨ���������ӿڷ���ĵ��ã� ������ת��Ϊ�����ڱ���װ�������ĵ��á�
5. **�ͻ��˴���ֻ��ͨ���ӿ����������������ɣ� ���������������������**�� ��ˣ� ��������������������͵��������������޸����д��롣 ���ڷ�����Ľӿڱ����Ļ��滻ʱ�����ã� �������޸Ŀͻ��˴���Ϳ��Դ����µ��������ࡣ

#### Coding

1. ����ͻ���ʹ�õĽӿڣ���ҵ�����

   ```java
   public interface Target {
   
       /*
        * �ͻ���������ķ���
        */
       void request();
   }
   ```

2. �Ѿ����ڵĽӿڣ�����ӿ���Ҫ����

   ```java
   public class Adaptee {
   
       /*
        * ԭ�����ڵķ���
        */
       public void specificRequest(){
       //ҵ�����
       }
   }
   ```

3. ��������

   ```java
   public class Adapter implements Target {
   
       /*
        * ������Ҫ������Ľӿڶ���
        */
       private Adaptee adaptee;
   
       /*
        * ���췽����������Ҫ������Ķ���
        * @param adaptee ��Ҫ������Ķ���
        */
       public Adapter(Adaptee adaptee) {
           this.adaptee = adaptee;
       }
   
       @Override
       public void request() {
           // TODO Auto-generated method stub
           adaptee.specificRequest();
       }
   
   }
   ```

4. ʹ���������Ŀͻ���

   ```java
   public class Client {
   
       public static void main(String[] args) {
           //������Ҫ������Ķ���
           Adaptee adaptee = new Adaptee();
           //�����ͻ�����Ҫ���õĽӿڶ���
           Target target = new Adapter(adaptee);
           //������
           target.request();
       }
   }
   ```



### ��������

��һʵ��ʹ���˼̳л��ƣ� ������ͬʱ�̳���������Ľӿڡ� ��ע�⣬ ���ַ�ʽ������֧�ֶ��ؼ̳еı��������ʵ�֣����� C++�� Java ��֧�ֶ��ؼ̳У�Ҳ��û�������������ˡ�

![���������ģʽ������������](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjtka91z8j31od0u0n9c.jpg)

**��������**����Ҫ��װ�κζ��� ��Ϊ��ͬʱ�̳��˿ͻ��˺ͷ������Ϊ�� ���书������д�ķ�������ɡ� ������ɵ���������������еĿͻ��������ʹ�á�

#### Coding

Java ��Ȼ����ʵ�ֱ�׼������������������һ�ֱ�ͨ�ķ�ʽ��Ҳ�ܹ�ʹ�ü̳���ʵ�ֽӿڵ����䣬�Ǿ�����������ȥʵ�� Target �Ľӿڣ�Ȼ��̳� Adaptee ��ʵ�֣���Ȼ����ʮ�ֱ�׼������˼��ࡣ

1. ������һ���Ѵ��ڵĽ����������

   ```java
   public class Adaptee {
       public void adapteeRequest() {
           System.out.println("�������ߵķ���");
       }
   }
   ```

2. ����ͻ���ʹ�õĽӿڣ���ҵ�����

   ```java
   public interface Target {
   
       void request();
   }
   ```

3. ��ô�ſ�����Ŀ��ӿ��е� `request()` ���� `Adaptee` �� `adapteeRequest()` �����أ�ֱ��ʵ�� `Target` �϶��ǲ��еģ���������ͨ��һ���������࣬ʵ�� `Target` �ӿڣ�ͬʱ�̳��� `Adaptee` �࣬Ȼ����ʵ�ֵ� `request()` �����е��ø���� `adapteeRequest()` ����

   ```java
   public class Adapter extends Adaptee implements Target{
       @Override
       public void request() {
           //...һЩ����...
           super.adapteeRequest();
           //...һЩ����...
       }
   }
   ```

4. ʹ���������Ŀͻ���

   ```java
   public class Client {
       public static void main(String[] args) {
   
           Target adapterTarget = new Adapter();
           adapterTarget.request();
       }
   }
   ```

   

##  ������ģʽ�ʺ�Ӧ�ó���

- ����ϣ��ʹ��ĳ���࣬ ������ӿ����������벻����ʱ�� ����ʹ���������ࡣ

- ������ģʽ�����㴴��һ���м���࣬ �����Ϊ�����������ࡢ ����������ṩ����ӿڵ���֮���ת������

- �������Ҫ��������һЩ�࣬ ���Ǵ���ͬһ���̳���ϵ�� �������������˶����һЩ��ͬ�ķ����� ������Щ��ͬ�ķ���������������һ�̳���ϵ�е����������еĹ��ԡ�

- �������չÿ�����࣬ ��ȱ�ٵĹ�����ӵ��µ������С� ���ǣ� ��������������������ظ������Щ���룬 ������ʹ�ô����л�ζ����

  ��ȱʧ������ӵ�һ��������������һ�����ŵö�Ľ�������� Ȼ������Խ�ȱ�ٹ��ܵĶ����װ���������У� �Ӷ���̬�ػ�ȡ���蹦�ܡ� ��Ҫ��һ������������ Ŀ�������Ҫ��ͨ�ýӿڣ� �������ĳ�Ա����Ӧ����ѭ��ͨ�ýӿڡ� ���ַ�ʽͬװ��ģʽ�ǳ����ơ�

### demo

��һ�������еĳ���������������������������ҹ����õ綼�� 220V�������ǵ��ֻ����һ����Ҫ 5V��

220V �Ľ������൱�ڱ������� Adaptee�����ǵ�Ŀ�� Target �� 5V ֱ���磬����������൱��һ�� Adapter����220V �������ѹ�任Ϊ 5V �����

1. ���������ǵ����õ磨�ҹ��� 220V����Ȼ���������������ҵ�����׼��������ʱ��չ��

   ```java
   public class Volatage220V {
   
       public final int output = 220;
   
       public int output220v() {
           System.out.println("�����ѹ " + output);
           return output;
       }
   }
   ```

2. ����ӿ�

   ```java
   public interface IVoltage5V {
        int output5V();
   }
   ```

3. ���ǵ��ֻ���磬ֻ֧�� 5V ��ѹ

   ```java
   public class Phone {
   
       public void charging(IVoltage5V v) {
           if (v.output5V() == 5) {
               System.out.println("��ѹ 5V �����ϳ���׼����ʼ���");
           } else {
               System.out.println("��ѹ�����ϱ�׼���޷����");
           }
       }
   }
   ```

4. ������

   ```java
   public class VoltageAdapter implements IVoltage5V {
   
       private Volatage220V volatage220V;  //�ۺ�
   
       public VoltageAdapter(Volatage220V v) {
           this.volatage220V = v;
       }
   
       @Override
       public int output5V() {
           int dst = 0;
           if (null != volatage220V) {
               int src = volatage220V.output220v();
               System.out.println("����������~~~~~");
               dst = src / 44;
               System.out.println("������������ɣ������ѹ" + dst);
           }
           return dst;
       }
   }
   ```

5. ���������ȥ�������Σ��в�ͬ�ĵ�ѹ��ֻ��Ҫ��չ���������ɡ�

   ```java
   public class Client {
       public static void main(String[] args) {
           Phone phone = new Phone();
           phone.charging(new VoltageAdapter(new Volatage220V()));
       }
   }
   ```



##  ������ģʽ��ȱ��

-  ��һְ��ԭ������Խ��ӿڻ�����ת������ӳ�����Ҫҵ���߼��з��롣
-  ����ԭ�� ֻҪ�ͻ��˴���ͨ���ͻ��˽ӿ������������н����� ������ڲ��޸����пͻ��˴����������ڳ�������������͵���������

-  �������帴�Ӷ����ӣ� ��Ϊ����Ҫ����һϵ�нӿں��ࡣ ��ʱֱ�Ӹ��ķ�����ʹ��������������ݻ���򵥡�



## Spring �е�������

Spring Դ�����ѹؼ���`Adapter` ����ֺܶ�ʵ���࣬SpringMVC �е� `HandlerAdapter` ��������������Ӧ�á�

�����Ȼع��� SpringMVC  �������̣�

![qsli.github.io](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjqoif1ddj30vq0ij0uq.jpg)

Spring MVC �е�������ģʽ��Ҫ����ִ��Ŀ�� `Controller` �е�����������

��Spring MVC�У�`DispatcherServlet` ��Ϊ�û���`HandlerAdapter` ��Ϊ�����ӿڣ������������ʵ�������ڶ�Ŀ����������䣬`Controller` ��Ϊ��Ҫ������ࡣ

ΪʲôҪ�� Spring MVC ��ʹ��������ģʽ��Spring MVC �е� `Controller` �����ڶ࣬��ͬ���͵� `Controller` ͨ����ͬ�ķ�������������д������������������ģʽ�Ļ���`DispatcherServlet` ֱ�ӻ�ȡ��Ӧ���͵� `Controller`����Ҫ���������жϣ���������δ���һ����

```java
if(mappedHandler.getHandler() instanceof MultiActionController){  
   ((MultiActionController)mappedHandler.getHandler()).xxx  
}else if(mappedHandler.getHandler() instanceof XXX){  
    ...  
}else if(...){  
   ...  
}  
```

�������������������һ�� Controller����Ҫ�ڴ����м���һ�� if ��䣬������ʽ��ʹ�ó�������ά����ҲΥ�������ģʽ�еĿ���ԭ�� �C ����չ���ţ����޸Ĺرա�

����ͨ��Դ�뿴�� SpringMVC �����ʵ�ֵģ����ȿ��º����� DispatcherServlet��

```java
public class DispatcherServlet extends FrameworkServlet {
  	//......
	//ά������HandlerAdapter��ļ���
    @Nullable
    private List<HandlerAdapter> handlerAdapters;
  
	//��ʼ��handlerAdapters
    private void initHandlerAdapters(ApplicationContext context) {
        this.handlerAdapters = null;
        if (this.detectAllHandlerAdapters) {
            Map<String, HandlerAdapter> matchingBeans = BeanFactoryUtils.beansOfTypeIncludingAncestors(context, HandlerAdapter.class, true, false);
            if (!matchingBeans.isEmpty()) {
                this.handlerAdapters = new ArrayList(matchingBeans.values());
                AnnotationAwareOrderComparator.sort(this.handlerAdapters);
            }
        } else {
            try {
                HandlerAdapter ha = (HandlerAdapter)context.getBean("handlerAdapter", HandlerAdapter.class);
                this.handlerAdapters = Collections.singletonList(ha);
            } catch (NoSuchBeanDefinitionException var3) {
            }
        }

        if (this.handlerAdapters == null) {
            this.handlerAdapters = this.getDefaultStrategies(context, HandlerAdapter.class);
            if (this.logger.isTraceEnabled()) {
                this.logger.trace("No HandlerAdapters declared for servlet '" + this.getServletName() + "': using default strategies from DispatcherServlet.properties");
            }
        }
    }
  
  //dispatch �����л��ȡ HandlerAdapter
  protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {
        //...
    
		//���controller��Ӧ��������
        HandlerAdapter ha = this.getHandlerAdapter(mappedHandler.getHandler());          
				
		//������������handler�����������󣬲�����ModelAndView
        mv = ha.handle(processedRequest, response, mappedHandler.getHandler());            
        //...
    }
  	
	  //���ض�Ӧ��controller�Ĵ�����
      protected HandlerAdapter getHandlerAdapter(Object handler) throws ServletException {
        if (this.handlerAdapters != null) {
            Iterator var2 = this.handlerAdapters.iterator();

            while(var2.hasNext()) {
                HandlerAdapter adapter = (HandlerAdapter)var2.next();
                if (adapter.supports(handler)) {
                    return adapter;
                }
            }
        }
    }
```

���ſ��� HandlerAdapter ��Դ�룬Ҳ�����������ӿ�:

```java
public interface HandlerAdapter {
    boolean supports(Object var1);

    @Nullable
    ModelAndView handle(HttpServletRequest var1, HttpServletResponse var2, Object var3) throws Exception;

    long getLastModified(HttpServletRequest var1, Object var2);
}
```



������һ��������̣�

1. �������������ӿ� DispatchServlet ����һ������ά�����е� HandlerAdapter����������ļ���û�ж��������������ã���ô DispatchServlet ���ڴ���ʱ�Ըñ������г�ʼ����ע������Ĭ�ϵ� HandlerAdapter��
2. ��һ���������ʱ��DispatchServlet ����ݴ������� handler ���ʹӸü�����Ѱ�Ҷ�Ӧ�� HandlerAdapter������д������ҵ������� `handler()` ����
3. ��Ӧ�� HandlerAdapter �е� `handler()` �����ֻ�ִ�ж�Ӧ Controller �� `handleRequest()` ����

�������� handler �ж�Ӧ��ϵ���������������ֶ����������ӿڵ�ʵ���࣬��ˣ����Ƕ���ѭ��ͬ����������׼�������û����԰�����ͬ�ķ�ʽ��ͨ����ͬ�� handler ȥ�������� ��Ȼ�ˣ�Spring �����ҲΪ���Ƕ�����һЩĬ�ϵ� Handler ��Ӧ����������

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfjrbrv96pj31ck0j0dl6.jpg)

ͨ��������ģʽ���ǽ����е� `controller` ͳһ���� `HandlerAdapter` ������ȥ��д������ `if-else`  ���� `Controller` �����жϣ�Ҳ��������չ�µ� `Controller` ���͡�



## �ο����л
��ͼ�� Java ���ģʽ��
��Head First���ģʽ��
https://refactoringguru.cn/design-patterns/
https://blog.csdn.net/lu__peng/article/details/79117894
https://juejin.im/post/5ba28986f265da0abc2b6084#heading-12
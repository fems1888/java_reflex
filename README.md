MainActivity里定义私有属性和方法
======
```java
.........
private String Str = "123";
	private String getName()
	{
		return Str;
	}
  ........
  ```
  在需要调用反射的地方使用如下方法
  ======
  ``` java
  try {
            Class<?> aClass = Class.forName("com.example.jpushdemo.MainActivity");//类名的完整路径 完整类名
            Object newInstance = aClass.newInstance();
            //直接获取私有属性的值
            Field str = aClass.getDeclaredField("Str");
            str.setAccessible(true);//设置可以访问
            Object o = str.get(newInstance);
            Log.e("=====&&&&", o.toString());

            //如果私有属性没有一开始赋值  通过私有方法获取值
            Method getName = aClass.getDeclaredMethod("getName");
            getName.setAccessible(true);
            Object invoke = getName.invoke(newInstance);
            Log.e("=====&&&&222", invoke.toString());
            
            //直接赋值并获取
            str.set(newInstance,"wsx");
            Log.e("=====&&&&333", str.get(newInstance).toString());


        } catch (Exception e) {
            e.printStackTrace();
        }
  ```

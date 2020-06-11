# 부 생성자: 상위 클래스를 다른 방식으로 초기화
생성자가 여럿 필요한 경우 가장 일반적인 상황은 프레임워크 클래스를 확장해야 하는데 여러 가지 방법으로 인스턴스를 초기화할 수 있게 다양한 생성자를 지원해야 하는 경우다.   
예를 들어 자바에서 선언된 생성자가 2개인 View 클래스가 있다고 가정해보자

<pre><code>
open class View{
  constructor(context: Context){  //------- 부 생성자
  
  }
  
  constructor(context: Context, attr: AttributeSet){   //------- 부 생성자
  
  }
}
</code></pre>

부 생성자는 constructor 키워드로 시작하는데 필요에 따라 얼마든지 부 생성자를 많이 생성해도 된다.   
그리고 이 클래스를 확정하면서 똑같이 부 생성자를 정의할 수 있다.

<pre><code>
class MyButton : View{
  constructor(context: Context)
    : super(context){  //------- 상위 클래스의 생성자 호출
  
  }
  
  constructor(context: Context, attr: AttributeSet){   //------- 상위 클래스의 생성자 호출
    : super(context, attr)
  
  }
}
</code></pre>

이렇게 해서 상위 클래스 생성자를 호출할 수 있다.
또한, 자바와 마찬가지로 생성자에서 this()를 통해 클래스 자신의 다른 생성자를 호출할 수 있다.

<pre><code>
class MyButton : View{
  constructor(context: Context) : this(context, MY_STYLE)
    : super(context){  //------- 이 클래스의 다른 생성자에게 위임한다.
  
  }
  
  constructor(context: Context, attr: AttributeSet) 
    : super(context, attr){
  
  }
}
</code></pre>

부 생성자가 필요한 주된 이유는 자바의 상호운용성때문이다. 그리고 클래스 인스턴스를 생성할 때 파라미터 목록이 다른 생성 방법이 여럿 존재하는 경우는 부 생성자를 여럿 둘 수밖에 없다.

다음 시간 - 인터페이스에 선언된 프로퍼티 구현

# Iterator 패턴
어떤 집합 객체를 순회하는 패턴 (내부 내용을 노출하지 않는 것이 포인트)  

![Iterator](Iterator.png)

장점  
* 집합객체가 어떤 구조(List,Set,Map) 되어 있는지 몰라도 된다(SRP, OCP)

단점  
* 구조가 복잡해 진다. -> 내부 구조가 변경될 가능성이 있을 때 사용할 것

```kolin:Iterator.kt
package iterator

import java.time.LocalDate

class Post(val title: String, val date: LocalDate) {
}

class Board {
  private val posts: MutableList<Post> = mutableListOf()
  fun addPost(post: Post) {
    posts.add(post)
  }
  fun getListIterator(): ListIterator {
    return ListIterator(posts)
  }
}

class ListIterator(posts: MutableList<Post>) : Iterator<Post> {
  val itr: Iterator<Post>
  init {
    this.itr = posts.iterator()
  }

  override fun hasNext(): Boolean {
    return itr.hasNext()
  }
  override fun next(): Post {
    return itr.next()
  }
}

fun main() {
  val board = Board()
  board.addPost(Post("디자인 패턴", LocalDate.now()))
  board.addPost(Post("디자인 패턴2", LocalDate.now()))
  board.addPost(Post("디자인 패턴3", LocalDate.now()))

  val postIterator = board.getListIterator()
  while(postIterator.hasNext()) {
    println(postIterator.next().title)
  }
}
```

1) Напишите дженерик класс вектор для математических векторов (кортеж) фиксированной длины 3, поддерживающий векторное сложение, вычитание, умножение/деление на скаляр, и скалярное произведение

````scala
case class Vector3[T: Numeric](x: T, y: T, z: T) {
  import Numeric.Implicits._

  def +(that: Vector3[T]): Vector3[T] = Vector3(x + that.x, y + that.y, z + that.z)

  def -(that: Vector3[T]): Vector3[T] = Vector3(x - that.x, y - that.y, z - that.z)

  def *(scalar: T): Vector3[T] = Vector3(x scalar, y scalar, z scalar)

  def /(scalar: T): Vector3[T] = Vector3(x / scalar, y / scalar, z / scalar)

  def dot(that: Vector3[T]): T = x * that.x + y * that.y + z * that.z

  def cross(that: Vector3[T]): Vector3[T] = Vector3(
    y * that.z - z * that.y,
  z *that.x - x * that.z,
  x * that.y - y * that.x
  )

  def magnitude(): Double = math.sqrt((x x + y y + z * z).toDouble)

  def normalize(): Vector3[Double] = {
    val mag = magnitude()
    Vector3(x.toDouble / mag, y.toDouble / mag, z.toDouble / mag)
  }
}
````


2. Напишите неявное преобразование ‘coerce’, которое конвертирует F[A] в F[B], при данном экземпляре функтора для F и неявного преобразования из A в B
```scala
implicit def coerce[F[_]: Functor, A, B](fa: F[A])(implicit ev: A => B): F[B] = 
  fa.map(ev)
```

3. Какие практики функционального програмирования вы использовали, пла, когда делали свой проект? (или планируете использовать при реализации проекта)
````text
композиция функции высшего порядка, функциональные примитивы, алгебраические типы - хз надеюсь вопрос про это

immutable объекты, однострочники, for-генераторы
````

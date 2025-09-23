Разбор компонентов
1. Абстрактный класс Metal (Металл)

          java
          public static abstract class Metal {
              public abstract int getEndurance();
          }

  1. abstract означает, что нельзя создать объект new Metal()
  2. Любой класс-наследник обязан реализовать метод getEndurance()
  3.Это "контракт" для всех металлов

2. Конкретные металлы

        java
        public static class Steel extends Metal { 
        public static class Copper extends Metal { 
        public static class Iron extends Metal {

Каждый металл наследует от Metal и реализует свою прочность.

5. Класс Plastic (Пластик)

        java
        public static class Plastic {
            // У пластика нет метода getEndurance()
        }

Этот класс НЕ наследуется от Metal, поэтому у него нет требуемого метода.

7. Класс Sword<T> (Меч) - самая важная часть

        java
        public static class Sword<T extends Metal> {
        <T extends Metal> означает: "тип T должен быть классом Metal или его наследником"

Это ограничение дженерика - компилятор не позволит создать Sword<Plastic>

      java
      public boolean checkDurability() {
          return this.swordMaterial.getEndurance() > 49;
      }

Мы можем вызывать getEndurance(), потому что компилятор знает: T гарантированно имеет этот метод (так как T extends Metal)

Почему важны дженерики с ограничениями
Что РАБОТАЕТ:

      java
      Sword<Steel> steelSword = new Sword<>(new Steel());
      Sword<Copper> copperSword = new Sword<>(new Copper());

Потому что Steel и Copper наследуются от Metal.

Что НЕ РАБОТАЕТ:

      java
      Sword<Plastic> plasticSword = new Sword<>(new Plastic());

Компилятор выдаст ошибку, потому что Plastic не extends Metal. Это защита на этапе компиляции!

Результат выполнения

    text
    Медный меч прошел проверку: нет     (20 < 49)
    Железный меч прошел проверку: нет   (30 < 49)  
    Стальной меч прошел проверку: да    (50 > 49)

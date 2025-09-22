# Java-Generics
Этот код демонстрирует работу с дженериками (обобщенными типами) и наследованием в Java. Вот подробное описание:
    
    public class Homework1 {
        public static abstract class Metal {
            public abstract int getEndurance();
        }
    
        public static class Steel extends Metal {
            @Override
            public int getEndurance() {
                return 50;
            }
        }
    
        public static class Copper extends Metal {
            @Override
            public int getEndurance() {
                return 20;
            }
        }
    
        public static class Iron extends Metal {
            @Override
            public int getEndurance() {
                return 30;
            }
        }
    
        public static class Plastic {
    
        }
    
        public static class Sword<T extends Metal> {
            T swordMaterial;
    
            public Sword(T swordMaterial) {
                this.swordMaterial = swordMaterial;
            }
    
            public boolean checkDurability() {
                return this.swordMaterial.getEndurance() > 49;
            }
        }
    
        public static void main(String[] args) {
            // System.out.println("Hello, World!");
    
            /*
            Компилятор будет ругаться
            Sword<Plastic> plasticSword = new Sword<>(new Plastic());
             */
    
            Sword<Copper> copperSword = new Sword<>(new Copper());
            Sword<Iron> ironSword = new Sword<>(new Iron());
            Sword<Steel> steelSword = new Sword<>(new Steel());
    
            System.out.println("Медный меч прошел проверку: " + (copperSword.checkDurability() ? "да" : "нет"));
            System.out.println("Железный меч прошел проверку: " + (ironSword.checkDurability() ? "да" : "нет"));
            System.out.println("Стальной меч прошел проверку: " + (steelSword.checkDurability() ? "да" : "нет"));
        }
    }

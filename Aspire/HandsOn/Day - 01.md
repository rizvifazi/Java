*Date : 04.01.2024*

Handson

Problem Statement:
Find out whether the following file will compile. If it does not compile, how you would fix it?

```java
public static void main(String[ ] args) {

      int x = 5;
      while (x > 1) {  
          x = x + 1;
          if (x < 3) {
               System.out.println(“small x”);
          }
      }
}
```

  The above will proceed till **(2^31)-1**, maximum value which can attain by `int`, once it reaches maximum value it will go to the minimum value **-(2^31)**




Problem Statement:

Find out whether the following file will compile. If it does not compile, how you would fix it?

  

                                                          class Digit {

      public static void main(String[ ] args) {

                                   int x = 1;

                                   while (x < 10) { 

                              if (x > 3) {

                                   System.out.println(“big x”);

                            }

                        }

                 }

            }

Problem Statement:

Find out whether the following file will compile. If it does not compile, how you would fix it?

  

                                                          class Loop {

                 public static void main(String[ ] args) {

                  int x = 5;

                             while (x  > 1) { 

                                   x = x - 1;

                        if (x < 3) {

                              System.out.println(“small x”);

                        }

                   }

             }

}

  
  

Problem Statement:

What is the output of the following program?

class Hexy {

     public static void main (String[] args)    {

         Integer i = 42;

         String s = (i<40)?"life":(i>50)?"universe":"everything";

         System.out.println(s);

    }

}

  

A.           null 

B.           life 

C.           universe 

D.          everything 

E.           Compilation fails 

F.           An exception is thrown at runtime.

Problem Statement:

Given:

1. class Example {    

2.     public static void main(String[] args) {

3.        Short s = 15;

4.        Boolean b;

5.        // insert code here

6.    }

7.}

  

Which, inserted independently at line 5, will compile? (Choose all that apply.)

A.           b  =  (Number instanceof s); 

B.           b  =  (s instanceof Short); 

C.           b  =  s.instanceof (Short); 

D.          b  =  (s.instanceof Number); 

E.           b  =  s.instanceof (Object); 

F.           b  =  (s instanceof String); 

Problem Statement:

What is the output of the following program?

class TryIt {

    public static void main(String[] args) {

        Integer x = 0;

        Integer y = 0;

       for(Short z = 0; z < 5; z++)

            if ((++x > 2) || (++y > 2))

                x++;

        System.out.println(x + " " + y);

    }

}

  
  

Problem Statement:

What is the output of the following program?

class Titanic {

    public static void main(String[] args)     {

        Boolean b1 = true;

        Boolean b2 = false;

        Boolean b3 = true;

        if ((b1 & b2) | (b2 & b3) & b3)

            System.out.println("alpha ");

        if ((b1 = false) | (b1 & b3) | (b1 | b2))

            System.out.println("beta ");

    }

}

  

a)       beta

b)      alpha

c)       alpha beta

d)      Compilation fails.

e)       No output is produced.

f)        An exception is thrown at runtime.

  

Problem Statement:

  

Given the following program:

1. class Maybe {    

2.     public static void main(String[] args) {

3.         boolean b1 = true;

4.         boolean b2 = false;

5.         System.out.println(!false ^ false);

6.         System.out.println(" " + (!b1 & (b2 = true)));

7.         System.out.println(" " + (b2 ^ b1));

8.     }

9. }

  

Which are true?

a)       Line 5 produces true.

b)      Line 5 produces false.

c)       Line 6 produces true.

d)      Line 6 produces false.

e)       Line 7 produces true.

f)        Line 7 produces false.

  

Problem Statement:

What is the output of the following program?

  

class Alien {

    String invade(short ships) {

        return " a few";

    }

}

  

class Defender {    

    public static void main(String[] args) {

        System.out.println(new Alien().invade(7));

    }

}

  

A.           many 

B.           a few 

C.           Compilation fails 

D.          The output is not predictable 

E.           An exception is thrown at runtime 

Problem Statement:

What is the output of the following program?

  

class Fizz {

   int x = 5;

    public static void main(String[] args) {

        final Fizz f1 = new Fizz();

        Fizz f2 = new Fizz();

        Fizz f3 = FizzSwitch(f1, f2);

        System.out.println((f1 == f3) + " " + (f1.x == f3.x));

    }

    static Fizz FizzSwitch(Fizz x, Fizz y) {

        final Fizz z = x;

        z.x = 6;

        return z;

    }

}

  

A.           true true 

B.           false true 

C.           true false 

D.          false false 

E.           Compilation fails. 

F.           An exception is thrown at runtime.
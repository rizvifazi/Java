
*Date : 04.15.2024*

01.	Interface II
1. Create an interface IPlayerStatistics
Add a method with the following prototype
public void displayPlayerStatistics

2. Create base class CricketPlayer
Include private data members : name, teamName, noOfMatches.
Include an 3 argument constructor with following arguments:  name, teamName, noOfMatches.
  
3. Create derived class Bowler  which extends  CricketPlayer and implements the interface  IplayerStatistics
Include private data members :  noOfWickets.
Include an 1 argument constructor with the argument:  noOfWickets and implement the interface method public void displayPlayerStatistics to display the player details.
  
4. Create derived  class Batsman  which extends  CricketPlayer and implements the interface  IPlayerStatistics
  Include private data members : runs.
  Include an 1 argument constructor with the argument: runs  and implement the interface method public void displayPlayerStatistics to display the player details.
  
5. Create derived class WicketKeeper  which extends  CricketPlayer and implements the interface  IPlayerStatistics
  Include private data members : noOfCatches, noOfStumpings ,runs,    noOfDismissals .
  Include an 4 argument constructor with following arguments:  noOfCatches, noOfStumpings,runs, noOfDismissals and implement the interface method public void displayPlayerStatistics to display the player details.
  
6. Create derived class AllRounder  which extends  CricketPlayer and implements the interface  IPlayerStatistics
  Include private data members : runs,noOfWickets.
  Include an 2 argument constructor with following arguments:  runs, noOfWickets  and implement the interface method public void displayPlayerStatistics to display the player details.
  
Create a Main class with main method to test test above classes. 
  
Input and Output Format:
Refer sample input and output for format specifications.
[All text in bold corresponds to input and the rest corresponds to output.]
  
Sample Input and Output 1:
Menu
1.Bowler
2.Batsman
3.WicketKeeper
4.AllRounder
Enter your choice
1
Enter the Bowler details
Enter player name
Ravichandran Ashwin
Enter team name
Chennai Super Kings
Enter number of matches played
111
Enter number of wickets taken
100
Player name : Ravichandran Ashwin
Team name : Chennai Super Kings
No of matches : 111
No of wickets taken : 100
Do you want to continue?
YES
Menu
1.Bowler
2.Batsman
3.WicketKeeper
4.AllRounder
Enter your choice
4
Enter the AllRounder details
Enter player name
Shane Watson
Enter team name
Royal Challengers Bangalore
Enter number of matches played
94
Enter the runs scored
2551
Enter number of wickets taken
81
Player name : Shane Watson
Team name : Royal Challengers Bangalore
No of matches : 94
Runs scored : 2551
No of wickets taken : 81
Do you want to continue?
NO
  
Sample Input and output 2:
Menu
1.Bowler
2.Batsman
3.WicketKeeper
4.AllRounder
Enter your choice
2
Enter the Batsman details
Enter player name
Virat Kohli
Enter team name
Royal Challengers Bangalore
Enter number of matches played
139
Enter the runs scored
4110
Player name : Virat Kohli
Team name : Royal Challengers Bangalore
No of matches : 139
Runs scored : 4110
Do you want to continue?
YES
Menu
1.Bowler
2.Batsman
3.WicketKeeper
4.AllRounder
Enter your choice
3
Enter the WicketKeeper details
Enter player name
Mahendra Singh Dhoni
Enter team name
Chennai Super Kings
Enter number of matches played
143
Enter number of catches taken
52
Enter number of stumpings
22
Enter number of dismissals
74
Enter the runs scored
3271
Player name : Mahendra Singh Dhoni
Team name : Chennai Super Kings
No of matches : 143
No of catches taken : 52
No of stumpings : 22
No of dismissals : 74
Runs scored : 3271
Do you want to continue?
NO
  


Problem Statement:
What is the output of the following program?
  
class Eggs {    
    int doX(Long x, Long y) { return 1;}
    int doX(long... x) { return 2;}
    int doX(Integer x, Integer y) { return 3; }
    int doX(Number n, Number m) { return 4; }
    public static void main(String[ ] args) {
        new Eggs().go();
    }
  
    void go() {
        short s = 7;
        System.out.println(doX(s,s) + " ");
        System.out.println(doX(7,7));
    }
}
  
A.           1  1 
B.           2  1 
C.           3  1 
D.          4  1 
E.           2  3 
F.           3  3 
G.          4  3 
  
Problem Statement:
What is the output of the following program?
  
class Mixer {    
    Mixer() { }
    Mixer(Mixer m) { m1 = m; }
    Mixer m1;
    public static void main(String[ ] args) {
        Mixer m2 = new Mixer();
        Mixer m3 = new Mixer(m2);
        m3.go();
        Mixer m4 = m3.m1;
        m4.go();
        Mixer m5 = m2.m1;
        m5.go();
    }
    void go() {
        System.out.println("hi ");
    }
}
  
  
  
Problem Statement:
What is the output of the following program?
  
class Bird {    
    { System.out.print("b1 "); }
    public Bird() {
        System.out.print("b2 ");
    }
}
  
class Raptor extends Bird {
    static { System.out.print("r1 "); }
    public Raptor() {
        System.out.print("r2 ");
    }
    { System.out.print("r3 "); }
    static { System.out.print("r4 "); }
}
  
class Hawk extends Raptor {
    public static void main(String[] args) {
        System.out.print("pre ");
        new Hawk();
        System.out.println("hawk ");
    }
}
  
A.           pre b1 b2 r3 r2 hawk 
B.           pre b2 b1 r2 r3 hawk 
C.           pre b2 b1 r2 r3 hawk r1 r4 
D.          r1 r4 pre b1 b2 r3 r2 hawk 
E.           r1 r4 pre b2 b1 r2 r3 hawk 
F.           pre r1 r4 b1 b2 r3 r2 hawk 
G.          pre r1 r4 b2 b1 r2 r3 hawk 
H.          The order of output cannot be predicted. 
I.            Compilation fails. 
  
  
  
Problem Statement:
What is the output of the following program?
  
class Clidders {
    public final void flipper() {
        System.out.println("Clidder");
    }
}
  
public class Clidlets  extends Clidders {
    public void flipper() {
        System.out.println("Flip a Clidlet");
        super.flipper();
    }    
    public static void main(String[] args) {
        new Clidlets().flipper();
    }    
}
  
A.           Flip a Clidlet 
B.           Flip  a Clidder 
C.           Flip a Clidder 
Flip a Clidlet
D.          Flip a Clidlet 
Flip a Clidder
E.           Compilation fails. 
  
  
Problem Statement:
Given the following:
  i.     interface Base {
ii.         boolean m1 ();
iii.         byte m2(short s);
iv.     }
  
Which code fragments will compile? (Choose all that apply.)
  
a)  interface Base2 implements Base { }
b)  abstract class Class2 extends Base {
    public boolean m1 ()  { return true; }  }
c)  abstract class Class2 implements Base { }
d)  abstract class Class2 implements Base {
   public boolean m1 () { return (true); }  }
e)  class Class2 implements Base {
  boolean m1 () { return false; }
  byte m2 (short s) { return 42; } }
  
  
Problem Statement:
Which of the following declare a compatible abstract class? (Choose all that apply.)
  
a)  public abstract class Canine { public Bark speak(); }
b)  public abstract class Canine { public Bark speak() { } }
c)  public class Canine { public abstract Bark speak(); }
d)  public class Canine abstract { public abstract Bark speak(); }
  
  
  
Problem Statement:
Given:
public abstract interface Frobnicate { public void twiddle(String s); }
  
Which is a correct class?
  
a)  public abstract void twiddle(String s) { }
}
b)  public abstract class Frob implements Frobnicate { }
c)  public class Frob extends Frobnicate {
              public void twiddle(Integer i) { }
}
d)  public class Frob implements Frobnicate {
            public void twiddle(Integer i) { }
}
e)  public class Frob implements Frobnicate {
             public void twiddle(String i) { }
             public void twiddle(Integer s) { }
}
  
  
Problem Statement:
Given:
1.      class Zing {
2.      protected Hmpf h;
3. }
4. class Woop extends Zing {  }
5. class Hmpf { }
  
Which is true?
A.     Woop IS-A Hmpf and HAS-A zing.
B.     Zing IS-A Woop and HAS-A Hmpf.
C.     Hmpf HAS-A Woop and Woop IS-A Zing.
D.    Woop HAS-A Hmpf and Woop IS-A Zing.
E.     Zing HAS-A Hmpf and Zing IS-A Woop.
  
  
Problem Statement:
Given:
            public class MyOuter {
         public static class MyInner { 
                    public static void foo() ) { } 
                }
           }
Which, if placed in a class other than MyOuter or MyInner, instantiates an instance of the nested class?
A.           MyOuter.MyInner m = new MyOuter.MyInner(); 
B.           MyOuter.MyInner m2 = new MyInner(); 
C.           MyOuter m = new MyOuter(); 
MyOuter.MyInner mi = m.new MyOuter.MyInner();
D.          MyInner mi = new MyOuter.MyInner(); 
Problem Statement:
What is the output of the following program?
  
public abstract class AbstractTest {
    public int getNum()) {
        return 45;
    }
    public abstract class Bar {
        public int getNum()) {
            return 38;
        }
   }
    public static void main()String[] args) {
        AbstractTest t = new AbstractTest()) {
            public int getNum()) {
                return 22;
            }
        };
        AbstractTest.Bar f = t.new Bar()) {
            public int getNum()) {
                return 57;
            }
        };
        System.out.println()f.getNum()) + " " + t.getNum()));
    }
}
  
A.           57  22 
B.           45  38 
C.           45  57 
D.          An exception occurs at runtime. 
E.           Compilation fails. 



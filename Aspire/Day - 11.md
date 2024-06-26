
*Date : 05.06.2024*


Streams API
    - contains collection of objects from some source(Array,List,Set) and process them sequentially
    - Collection framework also stores collection of object and we can manipulate the object, but with streams only used for processing the data and we cant manipulate the data 
    - present in java.util.stream.* package
    - 2 types of Streams - finite(fixed value) and infinite(unlimited values)
    - 2 types of operations
1. Intermediate operation - return stream itself - optional operation - we can chain multiple intermediate operation 
 - filter(), map(), flatMap(), sorted(), peek(), distinct(), limit(), skip()
2. Terminal operation - it will traverse into newly generated stream and return single value - mandatory operation - we cant chain terminal operation
- toArray(), forEach(), count(), min(), max(), reduce(), collect(), anyMatch(), allMatch(), noneMatch(), findFirst()

3 steps
Creation of Stream - Intermediate operation - Terminal operation
    - If we perform terminal operation then that stream is completely closed, so when we perform any other operation on closed stream then we get IllegalStateException

1. Creation of Stream(Finite stream) - 2 ways
1. stream() - used to generate a stream from some source called List or Set or Array

String[] s=new String[]{"one","two","three"};
Stream<String> st=s.stream();

List<Integer> l=new ArrayList<>();
l.add(3);
l.add(1);
l.add(4);
Stream<Integer> st1=l.stream();

2. of() - used to create our own stream

Stream<Integer> st2=Stream.of(1,2,3,4,5);

filter(Predicate) - intermediate - used to filter the data based on some condition

reduce() - terminal - used to reduce multiple values into single value
   - Optional reduce(BinaryOperator)
   - Integer reduce(int initialvalue, BinaryOperator)
   - Stream reduce(int initialvalue, BinaryOperator, BinaryOpeartor)

public class Main {
    public static void main(String[] args) {
      List<String> l=new ArrayList<>();
      l.add("Ram");
      l.add("Sam");
      l.add("Raj");
      l.add("Tam");
      l.add("Tim");
      l.add("John");
      l.add("Ram");
      l.add("Jack");
      System.out.println(l.size()); //8
      
      Stream<String> st=l.stream();
      Stream<String> st1=st.distinct();
      long val=st1.count();
      System.out.println(val); //7
      
      long val1=l.stream().distinct().count();
      System.out.println(val1); //7
      
      boolean b1=l.stream().distinct().anyMatch((e)->e.startsWith("R"));
      System.out.println(b1);  //true
      
      boolean b2=l.stream().distinct().allMatch((e)->e.startsWith("R"));
      System.out.println(b2);  //false
      
      boolean b3=l.stream().distinct().noneMatch((e)->e.startsWith("Z"));
      System.out.println(b3);  //true
      
      List<Student> l1=new ArrayList<>();
      l1.add(new Student(23,"PK"));
      l1.add(new Student(26,"KK"));
      l1.add(new Student(23,"MK")); 
      l1.add(new Student(21,"SK"));
      l1.add(new Student(40,"RK"));
      l1.add(new Student(30,"BK"));
      l1.add(new Student(29,"DK"));
      l1.add(new Student(28,"GK"));
      l1.add(new Student(33,"TK"));
      
      Stream<Student> st2=l1.stream().filter((e1)->e1.getId()>25);
      st2.forEach(System.out::println);
      
      Optional opt=Stream.of(3,5,6).reduce((a,b)->a*b);
      System.out.println(opt.get()); //90
      
      Integer i=Stream.of(3,5,6).reduce(2,(a,b)->a*b);
      System.out.println(i); //180
      
      Optional<String> opt1=Stream.of("lion","ape","tiger").min((c1,c2)->c1.length()-c2.length());
      System.out.println(opt1.get());  //ape
    }
}

map(Function) - intermediate - used for data transformation
              - take one Function functional interface as an argument and returns a stream consisting of results generated by applying the passed function to each element

collect() - terminal - used to collect the data as List or Set or Map

Collectors.toList()
Collectors.toSet()
Collectors.toMap(Function f1,Function f2)
Collectors.joining()
Collectors.counting()
Collectors.toCollection(Supplier)
Collectors.partitioningBy() - used to split the list based upon true or false condition
     - partitioningBy(Predicate)
     - partitioningBy(Predicate,Collector)
Collectors.groupingBy() - group the elements based on some condition
     - groupingBy(Function)
     - groupingBy(Function, Collector)
     - groupingBy(Function, Comparator, Collector)
Collectors.summarizingInt() - summarize all info like min, max, count, avg, sum

flatMap(Function) - intermediate
         - take one Function functional interface as an argument and returns a new stream and that stream is copied to another stream which will return the value

public class Main {
    public static void main(String[] args) {
       Integer[] a=new Integer[] {1,2,3,4,5};
       List<Integer> l1=Arrays.asList(a);
       
       //JDK10
       //List<Integer> l2=List.of(1,2,3,4,5);
       
       List<Integer> l2=l1.stream().map((e)->e*3).collect(Collectors.toList());
       l2.forEach(System.out::println); //3 6 9 12 15
       
       List<Integer> l3=l1.stream().flatMap((e1)->Stream.of(e1*2)).collect(Collectors.toList());
       System.out.println(l3); //[2,4,6,8,10]
       
       String s1=Stream.of("one","two","three").collect(Collectors.joining("-"));
       System.out.println(s1); //one-two-three
       
       long val=Stream.of("one","two","three").collect(Collectors.counting());
       System.out.println(val); //3
       
       List<String> l4=Stream.of("lions","tigers","bears","toads","toads")
              .filter((s)->s.startsWith("t")).collect(Collectors.toList());
       System.out.println(l4); //[tigers,toads,toads]
       
       List<String> l6=Stream.of("lions","tigers","bears","toads","toads")
               .filter((s)->s.startsWith("t")).distinct().collect(Collectors.toList());
        System.out.println(l6); //[tigers,toads]
       
       Set<String> l5=Stream.of("lions","tigers","bears","toads","toads")
               .filter((s)->s.startsWith("t")).collect(Collectors.toSet());
        System.out.println(l5); //[tigers,toads]
        
        TreeSet<String> l7=Stream.of("lions","tigers","bears","toads","toads","tadpoles")
                .filter((s)->s.startsWith("t")).collect(Collectors.toCollection(TreeSet::new));
         System.out.println(l7); //[tadpoles, tigers, toads]
         
         
         Map<String,Integer> hm=Stream.of("lions","tigers","bears","toads").collect(Collectors.toMap((k1)->k1, String::length));
         hm.forEach((k,v)->System.out.println("key = "+k+" value = "+v));
         
         
         Map<Boolean,List<String>> hm1=Stream.of("lions","tigers","bears","toads","toads","tadpoles")
             .collect(Collectors.partitioningBy((l)->l.length()<=5));
         System.out.println(hm1);
         
         Map<Boolean,Set<String>> hm2=Stream.of("lions","tigers","bears","toads","toads","tadpoles")
                 .collect(Collectors.partitioningBy((l)->l.length()<=5,Collectors.toSet()));
             System.out.println(hm2);
             
         Map<Integer,List<String>> hm3=Stream.of("lions","tigers","bears","lions","ape")
                 .collect(Collectors.groupingBy((e)->e.length()));
         System.out.println(hm3);
         
         Map<Integer,Set<String>> hm4=Stream.of("lions","tigers","bears","lions","ape")
                 .collect(Collectors.groupingBy((e)->e.length(),Collectors.toSet()));
         System.out.println(hm4);
         
         TreeMap<Integer,Set<String>> hm5=Stream.of("lions","tigers","bears","lions","ape")
                 .collect(Collectors.groupingBy((e)->e.length(),TreeMap::new, Collectors.toSet()));
         System.out.println(hm5);
    }
}

sorted() - intermediate - used to sort the elt

public class Main {
    public static void main(String[] args) {
      List<String> l11=List.of("9","A","z","1","B","4","e","f");
      
     List<String> l2=l11.stream().sorted().collect(Collectors.toList());
     System.out.println(l2); //[1, 4, 9, A, B, e, f, z] asc order
     
     List<String> l3=l11.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toList());
     System.out.println(l3); //desc order
     
     List<Student> l1=new ArrayList<>();
     l1.add(new Student(23,"PK"));
     l1.add(new Student(26,"KK"));
     l1.add(new Student(23,"MK")); 
     l1.add(new Student(21,"SK"));
     l1.add(new Student(40,"RK"));
     l1.add(new Student(30,"BK"));
     l1.add(new Student(29,"DK"));
     l1.add(new Student(28,"GK"));
     l1.add(new Student(33,"TK"));
     
     //comparingInt(),comparingDouble(), comparingLong()
    List<Student> l4=l1.stream().sorted(Comparator.comparingInt(Student::getId))
                .collect(Collectors.toList());
    l4.forEach(System.out::println);
    System.out.println();
    
    List<Student> l5=l1.stream().sorted(Comparator.comparing(Student::getName))
            .collect(Collectors.toList());
    l5.forEach(System.out::println); //name in asc order
    
    System.out.println();
    List<Student> l6=l1.stream().sorted(Comparator.comparing(Student::getName).reversed())
            .collect(Collectors.toList());
    l6.forEach(System.out::println); //name in desc order
    }
}

Other ways to create Stream
1. builder() - create finite stream
2. generate(Supplier) - create infinite stream
3. iterate(int initial,UnaryOperator) - create infinite stream

Create streams based on primitive datatype
1. IntStream - create stream of int values
2. DoubleStream - create stream of double values
3. LongStream - create stream of long values

From JDK1.9
takeWhile(Predicate) - if stream does not match the predicate,it will discard the rest of stream
dropWhile(Predicate) - if stream does not match the predicate,it will print the rest of stream


public class Main {
    public static void main(String[] args) {
        Stream<String> st=Stream.<String>builder().add("Ram").add("Sam").add("Raj").build();
        st.forEach(System.out::println);  //Ram Sam Raj
        
        Stream<Integer> st1=Stream.<Integer>builder().add(10).add(20).add(30).build();
        st1.forEach(System.out::println); //10 20 30
        
        Stream<String> st2=Stream.generate(()->"hello").limit(5);
        st2.forEach(System.out::println);
        
        Stream.iterate(2, (i)->i*2).skip(3).limit(5).forEach(System.out::println);
        
        IntStream i1=IntStream.range(1, 6); //start to end-1
        i1.forEach(System.out::println); //1 2 3 4 5
        
        IntStream i2=IntStream.rangeClosed(1, 6); //start to end
        i2.forEach(System.out::println); //1 2 3 4 5 6
        
        IntStream i3="abcd".chars();
        i3.forEach(System.out::println); //65 66 67 68
        
        Random r=new Random();
        DoubleStream d=r.doubles(5);
        d.forEach(System.out::println);
        
        List<Student> l1=new ArrayList<>();
        l1.add(new Student(23,"PK"));
        l1.add(new Student(26,"KK"));
        l1.add(new Student(23,"MK")); 
        l1.add(new Student(21,"SK"));
        l1.add(new Student(40,"RK"));
        l1.add(new Student(30,"BK"));
        l1.add(new Student(29,"DK"));
        l1.add(new Student(28,"GK"));
        l1.add(new Student(33,"TK"));
        
        IntStream i4=l1.stream().mapToInt(Student::getId);
        i4.forEach(System.out::println);
        
        OptionalInt op=l1.stream().mapToInt(Student::getId).max();
        System.out.println(op.getAsInt()); //40
        
        OptionalDouble op1=l1.stream().mapToDouble(Student::getId).average();
        System.out.println(op1.getAsDouble()); //28.111111111111
        
        //IntSummaryStatistics,DoubleSummaryStatistics,LongSummaryStatistics 
       IntSummaryStatistics i5=l1.stream().collect(Collectors.summarizingInt((t)->t.getId()));
       System.out.println(i5);
       System.out.println(i5.getAverage()+" "+i5.getCount());
       
       Stream.of(2,4,6,8,9,10,12).takeWhile((n)->n%2==0).forEach(System.out::println); //2 4 6 8
       Stream.of(2,4,6,8,9,10,12).dropWhile((n)->n%2==0).forEach(System.out::println); //9 10 12
    }
}
t

Parallel Stream
  - we want to access the stream elements parallelly
  - If we create stream using of(), then to access parallelly we have to use parallel()
  - If we create stream from some source, then to access parallelly we use parallelStream()

public class Main {
    public static void main(String[] args) {
       /*Stream.of(1,2,3,4,5,6,7,8,9).forEach((n)->{
                 System.out.println(Thread.currentThread().getName()+" "+n);
       });*/
      /* Stream.of(1,2,3,4,5,6,7,8,9).parallel().forEach((n)->{
                 System.out.println(Thread.currentThread().getName()+" "+n);
       });*/
              
              Stream.of(1,2,3,4,5,6,7,8,9).parallel().forEachOrdered((n)->{
                 System.out.println(Thread.currentThread().getName()+" "+n);
        });
              
              List<Integer> l1=List.of(1,2,3,4,5,6,7,8,9);
              l1.parallelStream().forEach((n)->{
                 System.out.println(Thread.currentThread().getName()+" "+n);
       });
       
    }
}

Java17
1. New method in Collectors class in Streams API 
   Collectors.teeing() - This accepts 2 collectors, each elt in the stream is processed by both collectors and then both their results are passed to merge function and transformed in to final result

Syntax: Collector teeing(Collector d1,Collector d2,BiFunction merger)

Stream.of(1,2,3,4,5).collect(Collectors.teeing(Collectors.minBy(Integer::compareTo),Collectors.maxBy(Integer::compareTo),(min,max)->min.get()+max.get()));   //6

Here we added min number with max number

2. Collectors.toList()

Stream.of("a","b","c").collect(Collectors.toList());  //old version
Stream.of("a","b","c").toList();  //Java17




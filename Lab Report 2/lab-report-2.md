## Week 2 Lab Report 

# Part 1: 
Last week we wrote code for a simple search engine. I wrote my code as follows: 

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    List<String> params = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add")) {
            String [] parameters = url.getQuery().split("=");
           if(parameters[1].equals("anewstringtoadd")){
               return "Add String to Query";
           }
           else{
                params.add(parameters[1]);
                return "String is added";
           }
        }
        else if(url.getPath().equals("/search")){
            String [] parameters = url.getQuery().split("=");
            String toreturn = "This search produced the words: ";
            for (String word: params){
                if(word.contains(parameters[1])){
                    toreturn = toreturn + word + " ";
                } 
            }
            return toreturn;
        }
        return "Error!!!";
    }
}

class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
Once compiled and ran, this code will act as a prototype search engine. It supports a path to add a new string to the list, and a path to query this list of strings and return a list of the strings that have a given substring. 

For example, when the path and query /add?s=anewstringtoadd is added to the url, this is the result: 
![](anewstringtoadd.png)
When this path is added, the handleRequest method in the code is called. The relevant arguments that this method will take into account is the path, /add, and the query ?s=anewstringtoadd. The method first checks if the path given is either /add or /search. If it is add, the method then looks at the query. If the query is ?s=anewstringtoadd it displays the text "Add String to Query" to the string. If not, and something else is added, that value is stored in an arraylist of strings for future reference. 

Next, I added the path and query /add?s=pineapple to the url and this was the result: 
![](pineapple.png)
Once again, when this path is added, the handleRequest method in the code is called. The relevant arguments that this method will take into account is the path, /add, and the query ?s=pineapple. The method first checks if the path given is either /add or /search. If it is add, the method then looks at the query. If the query is ?s=anewstringtoadd it displays the text "Add String to Query" to the string. In this case however this is not the query given. If something other than ?s=anewstringtoadd is given, that value is stored in an arraylist of strings for future reference and the program displays "String is added" to the screen. 

Next, I added the path and query /add?s=apple to the url and this was the result: 
![](apple.png)
This path and query does the exact same thing as the previous /add?s=pineapple, except apple is added to the arraylist of strings. 

Finally, I added the path and query /search?s=app. This was the result: 
![](search.png)
When this path is added, the handleRequest method in the code executes once again. The relevant arguments that this method will take into account is the path, /search, and the query ?s=app. The method first sees that the path is /search. Now it takes the query argument which in this case is "app" and checks if any of the strings saved in the arraylist of strings contains this substring. If they do have the substring, the program displays "This search produced the words: " followed by the words. 

# Part 2: 

In this week's lab, we were given many different files and asked to find the bugs within some of the methods. I have chosen to discuss the bug I found in the reverse method (ArrayExamples.java) and in the append method (LinkedListExamples.java). 

Reverse Method in ArrayExamples.java: 
- Failure Inducing Input
  The failure inducing input was performing a test where the method was given an array input that contained values, instead of an empty array. The array that I passed was {1,2,3}. I attached the code of my test below. 
  ```
  @Test
  public void testReversed2() {
    int[] input1 = {1,2,3};
    assertArrayEquals(new int[]{3,2,1}, ArrayExamples.reversed(input1));
  }
  ```
- Symptom
  The symptom was that at the 0th index, instead of the array value being 3, it was 0. I have shown what the output of the program looks like below. 
  ```
  1) testReversed2(ArrayTests)
  arrays first differed at element [0]; expected:<3> but was:<0>
    at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
    at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
    at org.junit.Assert.internalArrayEquals(Assert.java:534)
    at org.junit.Assert.assertArrayEquals(Assert.java:418)
    at org.junit.Assert.assertArrayEquals(Assert.java:429)
    at ArrayTests.testReversed2(ArrayTests.java:29)
    ... 32 trimmed
  ```
- The Bug
  First I will show what the original code for this method looked like. 
  ```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
  ```
  There are arguably two bugs in this code. The first bug is that in this line arr[i] = newArray[arr.length - i - 1], the reversed values are being assigned back to arr instead of the newarray. The second bug is in the return statement. The new array should be the one returned, not arr.  
  The fixed code looks like this: 
  ```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
  ```
- The connection
  In this code, newarray was never initialized to have the values of arr in the beginning, so it only contains the default value of 0 for all of its values. Therefore when this loop executes, arr's values all change to 0 so the array now looks like {0,0,0}. So finally when arr is returned, {0,0,0} is what is returned. This is why the symptom was that at the 0th index, the value was 0 instead of 3. 

Append Method in LinkedListExamples.java:
- Failure Inducing Input
  The failure inducing input was using the append method more than twice in order to have the append method go into its while loop. I have shown what my test looks like below. 
  ```
  @Test 
	public void testAppend() {
    LinkedList list1 = new LinkedList();
    list1.append(1);
    list1.append(3);
    list1.append(5);
    assertEquals(list1.root.next.next.value, 5);
	}
  ```
- The Symptom
  The symptom was that an out of memory error occurred. This indicates that the while loop ran infinetely. I have shown what the output of the program looked like below. 
  There was 1 failure:
  1) testAppend(LinkedListTests)
  java.lang.OutOfMemoryError: Java heap space
    at LinkedList.append(LinkedListExample.java:43)
    at LinkedListTests.testAppend(LinkedListTests.java:18)
- The Bug
  First I will show what the original code for this method looked like: 
  ```
  public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
    }
  ```
  The bug was that a new Node was being added everytime n.next != null. Since new nodes kept on being added, the loop never reached the end of the linked list and the loop ran infinetely until it ran out of memory. 
  Here is the fixed code: 
  ```
  public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
        }
        n.next = new Node(value, null);
    }
  ```
- The Connection
  n.next is only ever == null when the linked list is at the last element, because otherwise next will be pointing to the next element, not null. That is why the while loop was checkign for n.next!=null. However the creation of the appended Node should not have been happening within the while loop because that would mean a new Node being created at every iteration instead of one new Node being created at the end of the list. Since new nodes kept being created, the while loop never stopped running. The fix for this was to put the line for the creationn of the new node outside of the while loop, once the loop had iterated to the end of the list. 







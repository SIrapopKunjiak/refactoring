# Refactoring Assignment

From Siravit's Covid-19 tracker code: https://github.com/Kuea666/Covid-19-Tracker666

### reader() method
In the `/src/cv19Tracker/strategy/ReadTextStrategy.java` class

https://github.com/Kuea666/Covid-19-Tracker666/blob/master/src/cv19Tracker/strategy/ReadTextStrategy.java

consider this code:
```java
 public String[] reader(String urlString) {
    StringBuilder stringBuilder = new StringBuilder(); //create an object of StringBuilder
    try {
        URL url = new URL(urlString);
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(url.openStream()));
        String line;
        while ((line = bufferedReader.readLine()) != null) {
            stringBuilder.append(line);
            stringBuilder.append(System.getProperty("line.separator"));
        }
        bufferedReader.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
    String s =stringBuilder.toString();
    s=s.substring(1,s.length()-2);
    String[] splitStringArray = s.split(",");

    return splitStringArray;
    }
```
* Refactoring Signs:
  - The Method is too long.It's hard to figure out what the method does.
 
* Refactoring: Extract the method to two method.  
```java
public String[] reader(String urlString) {
        createString(urlString);
        String s = null;
        s=s.substring(1,s.length()-2);
    String[] splitStringArray = s.split(",");

    return splitStringArray;
    }

    static void buildString(String urlString) {
        StringBuilder stringBuilder = new StringBuilder(); //create an object of StringBuilder
        try {
            URL url = new URL(urlString);
            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(url.openStream()));
            String line;
            while ((line = bufferedReader.readLine()) != null) {
                stringBuilder.append(line);
                stringBuilder.append(System.getProperty("line.separator"));
            }
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        String s =stringBuilder.toString();
    }
```
```java
public class ArrayBox {
    private static final int DEFAULT_CAPACITY = 10;
    public int[] elementData;
    private int size = 0;//有效元素个数

    public ArrayBox(){
        elementData = new int[DEFAULT_CAPACITY];
    }
    public ArrayBox(int capacity){
        elementData = new int[capacity];
    }
    public boolean add(int element){
        this.ensureCap(size + 1);
        elementData[size++] = element;
        return true;
    }
    public int get(int index){
        this.checkIndex(index);
        return elementData[index];
    }
    //删除元素给用户还回去
    public int remove(int index){
        this.checkIndex(index);
        int rn = elementData[index];
        elementData = this.rmdArray(elementData, index);
        return rn;
    }
    public int getSize(){
        return this.size;
    }

    private int[] rmdArray(int[] array, int index){
        for(int i=index; i<size-1; i++){
            array[index] = array[index+1];
        }
        array[--size] = 0;
        return array;
    }

    public void checkIndex(int index){
        if(index<0 || index>=size){
            throw new BoxIndexOutOfBoundsException("index:"+index+", size:"+size);
        }
    }
    private void ensureCap(int minCap){
        if(minCap > elementData.length){
            this.grow(minCap);
        }
    }
    // 扩容
    private void grow(int minCap){
        int oldCap = elementData.length;
        int newCap = oldCap + (oldCap >> 1); //1.5倍
        if(newCap - minCap < 0){
            newCap = minCap;
        }
        elementData = this.copyOf(elementData, newCap);
    }

    private int[] copyOf(int[] oldArray, int newCap){
        int[] newArray = new int[newCap];
        for(int i=0; i<oldArray.length;i++){
            newArray[i] = oldArray[i];
        }
        return newArray;
    }

}

```





```java
public class BoxIndexOutOfBoundsException extends RuntimeException {//继承extends  实现类implements
    public BoxIndexOutOfBoundsException(){}
    public BoxIndexOutOfBoundsException(String msg){
        super(msg);//把msg提供给父类
    }
}

```





```java
public class Demo{
    public static void main (String[] args){
        ArrayBox b = new ArrayBox();
        for(int i=1; i<=10; i++){
            b.add(10*i);
        }
        System.out.println(b.getSize());
        System.out.println(b.elementData.length);
        //访问
        int v = b.get(9);
        System.out.println(v);
        //遍历
        for(int i=0;i<b.getSize();i++){
            System.out.print(b.get(i)+" ");
        }
        System.out.println();
        int rm = b.remove(2);
        for(int i=0;i<b.getSize();i++){
            System.out.print(b.get(i)+" ");
        }
    }
}

//输出：
10
10
100
10 20 30 40 50 60 70 80 90 100 
10 20 40 40 50 60 70 80 90 
```


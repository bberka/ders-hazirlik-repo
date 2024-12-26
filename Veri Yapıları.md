# Tek Yönlü Bağlı Liste (Singly Linked List)

## Tanım
Tek yönlü bağlı liste (singly linked list), her elemanının (düğüm) bir sonraki elemanın adresini (referansını) tutarak birbirine bağlandığı bir veri yapısıdır. Bu yapı, liste üzerinde dinamik bellek kullanımı sağlar ve eleman ekleme ya da silme işlemleri kolayca yapılabilir.

Tek yönlü bağlı listenin her düğümü, iki bileşenden oluşur:
- **Veri (Data)**: Düğümde saklanan değer.
- **Sonraki (Next)**: Bir sonraki düğümün adresi (referansı).

Son düğümün **Next** bileşeni genellikle `null` olur, çünkü son düğümün bağlantısı yoktur.

## Avantajları
- Dinamik büyüyüp küçülmesi sayesinde sabit boyutlu dizilere göre daha esnektir.
- Eleman eklemek ve silmek kolaydır, çünkü sadece bağlantılar değiştirilir.

## Dezavantajları
- Bağlantılar üzerinde gezinme, indeksli erişim kadar hızlı değildir (zaman karmaşıklığı O(n)).
- Her eleman ek olarak bellek kullanır (veri ve bağlantı).

## Temel İşlemler
1. **Başlangıçtan Ekleme**: Yeni bir düğüm, listenin başına eklenir.
2. **Sondan Ekleme**: Yeni bir düğüm, listenin sonuna eklenir.
3. **Silme**: Belirli bir düğüm listeden silinir.
4. **Arama**: Belirli bir değeri içeren düğüm bulunur.
5. **Listeyi Yazdırma**: Listenin elemanları yazdırılır.

## C# ile Tek Yönlü Bağlı Liste Uygulaması

### Düğüm Sınıfı (Node)
İlk olarak, bağlı listenin her elemanını temsil edecek bir `Node` sınıfı tanımlarız. Bu sınıf, veriyi ve bir sonraki düğümü (bağlantıyı) tutar.

```csharp
public class Node
{
    public int Data;  // Düğümün verisi
    public Node Next; // Bir sonraki düğümün referansı

    // Constructor
    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}


```

### Tek Yönlü Bağlı Liste Sınıfı 
Bağlı listeyi yönetmek için bir sınıf oluştururuz. Bu sınıf, başlangıç noktasına (head) ve listeyi yönetmeye yönelik fonksiyonlara sahiptir.
```csharp
public class SinglyLinkedList
{
    private Node head; // Listenin ilk düğümü

    // Constructor
    public SinglyLinkedList()
    {
        head = null;
    }

    // Listenin başına yeni bir düğüm ekler
    public void AddFirst(int data)
    {
        Node newNode = new Node(data);
        newNode.Next = head;
        head = newNode;
    }

    // Listenin sonuna yeni bir düğüm ekler
    public void AddLast(int data)
    {
        Node newNode = new Node(data);
        if (head == null)
        {
            head = newNode;
        }
        else
        {
            Node current = head;
            while (current.Next != null)
            {
                current = current.Next;
            }
            current.Next = newNode;
        }
    }

    // Listeyi yazdırır
    public void PrintList()
    {
        Node current = head;
        while (current != null)
        {
            Console.Write(current.Data + " ");
            current = current.Next;
        }
        Console.WriteLine();
    }

    // Belirli bir değeri listede arar
    public bool Search(int data)
    {
        Node current = head;
        while (current != null)
        {
            if (current.Data == data)
                return true;
            current = current.Next;
        }
        return false;
    }

    // İlk düğümü listeden siler
    public void DeleteFirst()
    {
        if (head != null)
        {
            head = head.Next;
        }
    }

    // Listeyi tersine çevirir
    public void Reverse()
    {
        Node prev = null;
        Node current = head;
        Node next = null;
        
        while (current != null)
        {
            next = current.Next;
            current.Next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }
}

```

### Zaman Karmaşıklığı
- AddFirst: O(1)
- AddLast: O(n) (Son düğüme erişmek için listenin sonuna kadar gitmek gerekir)
- DeleteFirst: O(1)
- Search: O(n)
- Reverse: O(n)


# Çift Yönlü Bağlı Liste (Doubly Linked List)

## Tanım
Çift yönlü bağlı liste, her elemanının (düğüm) hem bir sonraki hem de bir önceki elemanın adresini tutarak birbirine bağlandığı bir veri yapısıdır. Bu yapının her düğümü, iki bağlantıya (yani iki pointer'a) sahiptir: biri bir sonraki düğüme (`Next`), diğeri bir önceki düğüme (`Prev`). Bu, veri üzerinde daha esnek gezinme sağlar, çünkü her düğüm hem ileri hem de geri yönde erişilebilir.

### Düğüm Yapısı
Her düğüm, üç bileşenden oluşur:
- **Veri (Data)**: Düğümde saklanan değer.
- **Sonraki (Next)**: Bir sonraki düğümün adresi (referansı).
- **Önceki (Prev)**: Bir önceki düğümün adresi (referansı).

### Avantajları
- Bağlantılar üzerinden ileri ve geri yönlü gezinme sağlanır, bu da bazı işlemleri hızlandırabilir.
- Listeyi hem baştan hem de sondan değiştirmek kolaydır.
- Eleman eklemek ve silmek hızlıdır.

### Dezavantajları
- Daha fazla bellek gerektirir, çünkü her düğüm iki referansa sahip olur (bir sonraki ve bir önceki düğüm için).
- Kod karmaşıklığı daha fazladır, çünkü hem ileri hem de geri yönlü bağlantılar yönetilmelidir.

## Temel İşlemler
1. **Başlangıçtan Ekleme**: Yeni bir düğüm, listenin başına eklenir.
2. **Sondan Ekleme**: Yeni bir düğüm, listenin sonuna eklenir.
3. **Silme**: Belirli bir düğüm listeden silinir.
4. **Arama**: Belirli bir değeri içeren düğüm bulunur.
5. **Listeyi Yazdırma**: Listenin elemanları yazdırılır.

## C# ile Çift Yönlü Bağlı Liste Uygulaması

### Düğüm Sınıfı (Node)
İlk olarak, bağlı listenin her elemanını temsil edecek bir `Node` sınıfı tanımlarız. Bu sınıf, veriyi, bir sonraki düğümü ve bir önceki düğümü tutar.

```csharp
public class Node
{
    public int Data;  // Düğümün verisi
    public Node Next; // Bir sonraki düğümün referansı
    public Node Prev; // Bir önceki düğümün referansı

    // Constructor
    public Node(int data)
    {
        Data = data;
        Next = null;
        Prev = null;
    }
}
```

```csharp
public class DoublyLinkedList
{
    private Node head; // Listenin ilk düğümü
    private Node tail; // Listenin son düğümü

    // Constructor
    public DoublyLinkedList()
    {
        head = null;
        tail = null;
    }

    // Listenin başına yeni bir düğüm ekler
    public void AddFirst(int data)
    {
        Node newNode = new Node(data);
        if (head == null) // Liste boşsa
        {
            head = tail = newNode;
        }
        else
        {
            newNode.Next = head;
            head.Prev = newNode;
            head = newNode;
        }
    }

    // Listenin sonuna yeni bir düğüm ekler
    public void AddLast(int data)
    {
        Node newNode = new Node(data);
        if (tail == null) // Liste boşsa
        {
            head = tail = newNode;
        }
        else
        {
            newNode.Prev = tail;
            tail.Next = newNode;
            tail = newNode;
        }
    }

    // Listeyi yazdırır (Başlangıçtan sona)
    public void PrintListForward()
    {
        Node current = head;
        while (current != null)
        {
            Console.Write(current.Data + " ");
            current = current.Next;
        }
        Console.WriteLine();
    }

    // Listeyi yazdırır (Sondan başa)
    public void PrintListBackward()
    {
        Node current = tail;
        while (current != null)
        {
            Console.Write(current.Data + " ");
            current = current.Prev;
        }
        Console.WriteLine();
    }

    // Belirli bir değeri listede arar
    public bool Search(int data)
    {
        Node current = head;
        while (current != null)
        {
            if (current.Data == data)
                return true;
            current = current.Next;
        }
        return false;
    }

    // İlk düğümü listeden siler
    public void DeleteFirst()
    {
        if (head != null)
        {
            if (head == tail) // Liste tek elemanlıysa
            {
                head = tail = null;
            }
            else
            {
                head = head.Next;
                head.Prev = null;
            }
        }
    }

    // Son düğümü listeden siler
    public void DeleteLast()
    {
        if (tail != null)
        {
            if (head == tail) // Liste tek elemanlıysa
            {
                head = tail = null;
            }
            else
            {
                tail = tail.Prev;
                tail.Next = null;
            }
        }
    }
}
```
### Zaman Karmaşıklıkları
- AddFirst: O(1)
- AddLast: O(1)
- DeleteFirst: O(1)
- DeleteLast: O(1)
- Search: O(n)




# Yığın (Stack) Yapıları

Yığın (Stack), **LIFO (Last In, First Out)** prensibine göre çalışan bir veri yapısıdır. Bu prensibe göre son eklenen eleman, ilk çıkarılır.

## Yığın Özellikleri
- **Push:** Yığına eleman ekler.
- **Pop:** Yığından eleman çıkarır.
- **Peek:** Yığının en üstündeki elemanı görüntüler.
- **IsEmpty:** Yığının boş olup olmadığını kontrol eder.

## Yığınların Temsili
Yığınlar, genellikle iki şekilde temsil edilir:
1. **Dizi (Array) Temsili**
2. **Bağlı Liste (Linked List) Temsili**

---

## 1. Dizi Şeklinde Yığın

Dizi kullanarak yığın, sabit bir kapasiteye sahiptir ve bu kapasiteyi aşarsa taşma (overflow) durumu oluşur.

### C# Kod Örneği
```csharp
class ArrayStack
{
    private int[] stack;
    private int top;
    private int capacity;

    public ArrayStack(int size)
    {
        stack = new int[size];
        capacity = size;
        top = -1;
    }

    public void Push(int item)
    {
        if (top == capacity - 1)
        {
            Console.WriteLine("Yığın dolu! (Overflow)");
            return;
        }
        stack[++top] = item;
    }

    public int Pop()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Yığın boş! (Underflow)");
            return -1;
        }
        return stack[top--];
    }

    public int Peek()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Yığın boş!");
            return -1;
        }
        return stack[top];
    }

    public bool IsEmpty()
    {
        return top == -1;
    }
}
```

### Kullanım
```csharp
var stack = new ArrayStack(5);
stack.Push(10);
stack.Push(20);
Console.WriteLine(stack.Peek()); // Çıktı: 20
Console.WriteLine(stack.Pop());  // Çıktı: 20
Console.WriteLine(stack.IsEmpty()); // Çıktı: False
```

---

## 2. Bağlı Liste Şeklinde Yığın

Bağlı liste ile temsil edilen yığın, dinamik bir yapıya sahiptir ve kapasite sınırı yoktur (hafıza izin verdiği sürece).

### C# Kod Örneği
```csharp
class LinkedListStack
{
    private class Node
    {
        public int Data;
        public Node Next;

        public Node(int data)
        {
            Data = data;
            Next = null;
        }
    }

    private Node top;

    public LinkedListStack()
    {
        top = null;
    }

    public void Push(int item)
    {
        Node newNode = new Node(item);
        newNode.Next = top;
        top = newNode;
    }

    public int Pop()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Yığın boş! (Underflow)");
            return -1;
        }
        int popped = top.Data;
        top = top.Next;
        return popped;
    }

    public int Peek()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Yığın boş!");
            return -1;
        }
        return top.Data;
    }

    public bool IsEmpty()
    {
        return top == null;
    }
}
```

### Kullanım
```csharp
var stack = new LinkedListStack();
stack.Push(10);
stack.Push(20);
Console.WriteLine(stack.Peek()); // Çıktı: 20
Console.WriteLine(stack.Pop());  // Çıktı: 20
Console.WriteLine(stack.IsEmpty()); // Çıktı: False
```

---

## 3. Yığın Uygulamaları

### Parantez Denge Kontrolü
Bir ifade içindeki parantezlerin doğru şekilde kapanıp kapanmadığını kontrol etmek için yığın kullanılabilir.

### C# Kod Örneği
```csharp
bool IsBalanced(string expression)
{
    Stack<char> stack = new Stack<char>();

    foreach (char ch in expression)
    {
        if (ch == '(' || ch == '{' || ch == '[')
        {
            stack.Push(ch);
        }
        else if (ch == ')' || ch == '}' || ch == ']')
        {
            if (stack.Count == 0)
                return false;

            char top = stack.Pop();
            if ((ch == ')' && top != '(') ||
                (ch == '}' && top != '{') ||
                (ch == ']' && top != '['))
            {
                return false;
            }
        }
    }

    return stack.Count == 0;
}
```

### Kullanım
```csharp
Console.WriteLine(IsBalanced("{[()]}")); // Çıktı: True
Console.WriteLine(IsBalanced("{[(])}")); // Çıktı: False
```

---

## Özet
- **Dizi şeklinde yığın:** Sabit kapasiteye sahip, hafıza açısından daha basit.
- **Bağlı liste şeklinde yığın:** Dinamik kapasiteye sahip, eleman ekleme ve çıkarma daha esnek.
- **Uygulamalar:** Parantez dengesi, geri alma işlemleri, DFS gibi birçok alanda kullanılır.
---


# Kuyruk Yapıları (Queue Structures)

## Tanım
Kuyruk, **FIFO (First In, First Out)** prensibine dayalı bir veri yapısıdır. Yani, ilk eklenen eleman ilk olarak çıkar. Kuyruklar, verilerin sıralı bir şekilde işlendiği sistemlerde yaygın olarak kullanılır. Örneğin, işlem sırasındaki taleplerin sırasıyla işlenmesi, baskı kuyruğu, bekleme sırasındaki çağrılar gibi senaryolarda kullanılır.

Kuyruk yapısında üç ana işlem vardır:
- **Enqueue**: Kuyruğa eleman eklemek.
- **Dequeue**: Kuyruktan eleman çıkarmak.
- **Peek** (Front): Kuyruğun önündeki elemana erişmek.

Kuyruklar genellikle iki uçlu yapılardır: bir **ön** (front) ve bir **son** (rear). Elemanlar **sondan** eklenir ve **önden** çıkarılır.

## Temel Kuyruk İşlemleri
1. **Enqueue**: Kuyruğun sonuna yeni bir eleman ekler.
2. **Dequeue**: Kuyruğun başından bir eleman çıkarır.
3. **Peek**: Kuyruğun başındaki elemanı görür, ancak çıkarmaz.
4. **IsEmpty**: Kuyruğun boş olup olmadığını kontrol eder.
5. **Size**: Kuyruğun kaç eleman içerdiğini gösterir.

## C# ile Kuyruk Uygulaması (Array ile)

Aşağıda, sabit boyutlu bir dizi kullanarak kuyruğun nasıl oluşturulacağı ve temel işlemlerin nasıl yapılacağı gösterilmektedir.

```csharp
public class Queue
{
    private int[] elements;
    private int front;
    private int rear;
    private int size;
    private int capacity;

    public Queue(int capacity)
    {
        this.capacity = capacity;
        elements = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    // Kuyruğa eleman ekler
    public void Enqueue(int element)
    {
        if (size == capacity)
        {
            Console.WriteLine("Queue is full");
            return;
        }
        rear = (rear + 1) % capacity;  // Dairesel kuyruk mantığı
        elements[rear] = element;
        size++;
    }

    // Kuyruktan eleman çıkarır
    public int Dequeue()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        int element = elements[front];
        front = (front + 1) % capacity; // Dairesel kuyruk mantığı
        size--;
        return element;
    }

    // Kuyruğun başındaki elemanı görür
    public int Peek()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        return elements[front];
    }

    // Kuyruğun boş olup olmadığını kontrol eder
    public bool IsEmpty()
    {
        return size == 0;
    }

    // Kuyruğun boyutunu döndürür
    public int Size()
    {
        return size;
    }
}
```

### Dairesel Kuyruk Uygulaması
```csharp
public class CircularQueue
{
    private int[] elements;
    private int front;
    private int rear;
    private int size;
    private int capacity;

    public CircularQueue(int capacity)
    {
        this.capacity = capacity;
        elements = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    // Kuyruğa eleman ekler
    public void Enqueue(int element)
    {
        if (size == capacity)
        {
            Console.WriteLine("Queue is full");
            return;
        }
        rear = (rear + 1) % capacity;  // Dairesel kuyruk mantığı
        elements[rear] = element;
        size++;
    }

    // Kuyruktan eleman çıkarır
    public int Dequeue()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        int element = elements[front];
        front = (front + 1) % capacity; // Dairesel kuyruk mantığı
        size--;
        return element;
    }

    // Kuyruğun başındaki elemanı görür
    public int Peek()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        return elements[front];
    }

    // Kuyruğun boş olup olmadığını kontrol eder
    public bool IsEmpty()
    {
        return size == 0;
    }

    // Kuyruğun boyutunu döndürür
    public int Size()
    {
        return size;
    }
}
```

### C# İle Bağlı Liste Kuyruk Yapısı
```csharp
public class Node
{
    public int Data;
    public Node Next;

    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}

public class QueueWithLinkedList
{
    private Node front;
    private Node rear;
    private int size;

    public QueueWithLinkedList()
    {
        front = rear = null;
        size = 0;
    }

    // Kuyruğa eleman ekler
    public void Enqueue(int element)
    {
        Node newNode = new Node(element);
        if (rear == null)
        {
            front = rear = newNode;
        }
        else
        {
            rear.Next = newNode;
            rear = newNode;
        }
        size++;
    }

    // Kuyruktan eleman çıkarır
    public int Dequeue()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        int element = front.Data;
        front = front.Next;
        if (front == null)
        {
            rear = null;
        }
        size--;
        return element;
    }

    // Kuyruğun başındaki elemanı görür
    public int Peek()
    {
        if (IsEmpty())
        {
            Console.WriteLine("Queue is empty");
            return -1;
        }
        return front.Data;
    }

    // Kuyruğun boş olup olmadığını kontrol eder
    public bool IsEmpty()
    {
        return size == 0;
    }

    // Kuyruğun boyutunu döndürür
    public int Size()
    {
        return size;
    }
}
```
---

# Özyinelemeli Fonksiyonlar ve Uygulamaları

## Tanım
Özyinelemeli fonksiyonlar, bir fonksiyonun kendi kendisini çağırdığı fonksiyonlardır. Bu teknik, genellikle belirli problemlerin daha küçük parçalara bölünerek çözülmesi gerektiğinde kullanılır. Özyineleme, çözüm sürecini adım adım daraltarak problemi daha küçük alt problemlere indirger.

Bir özyinelemeli fonksiyonun çalışabilmesi için:
- **Temel durum (Base case)** olmalıdır: Bu durum, özyinelemenin duracağı ve sorunun doğrudan çözüleceği durumdur.
- **Özyineleme adımı (Recursive step)** olmalıdır: Fonksiyon, her çağrısında kendi problemini daha küçük bir problemle çözmeye çalışır.

### Özyineleme Yapısı
Bir özyinelemeli fonksiyon şu şekilde yapılandırılabilir:
1. **Base case**: Fonksiyonun duracağı nokta. Bu, fonksiyonun kendisini çağırmayı bıraktığı ve çözümün bulunmaya başlandığı durumdur.
2. **Recursive case**: Fonksiyonun kendi kendisini çağırdığı durumdur. Bu adım, çözümü daha küçük bir alt problem olarak devam ettirir.

## C# ile Özyinelemeli Fonksiyonlar

### Özyinelemeli Faktöriyel Hesaplama

Faktöriyel, genellikle özyinelemeli fonksiyonlarla hesaplanabilen klasik bir örnektir. Faktöriyel, bir pozitif tamsayı n için `n! = n * (n-1) * (n-2) * ... * 1` şeklinde tanımlanır.

**Faktöriyel Özyinelemeli Fonksiyonu**:

```csharp
public class RecursionExamples
{
    // Faktöriyel hesaplama (n! = n * (n-1) * (n-2) * ... * 1)
    public static int Factorial(int n)
    {
        // Base case: 0! ve 1! her ikisi de 1'dir
        if (n == 0 || n == 1)
        {
            return 1;
        }
        // Recursive case: n! = n * (n-1)!
        return n * Factorial(n - 1);
    }

    public static void Main(string[] args)
    {
        int number = 5;
        Console.WriteLine($"{number}! = {Factorial(number)}");  // Çıktı: 120
    }
}
```

**Fibonacci Özyinelemeli Fonksiyonu:**
```csharp
public class RecursionExamples
{
    // Fibonacci hesaplama (F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2))
    public static int Fibonacci(int n)
    {
        // Base case: F(0) = 0, F(1) = 1
        if (n == 0)
        {
            return 0;
        }
        else if (n == 1)
        {
            return 1;
        }
        // Recursive case: F(n) = F(n-1) + F(n-2)
        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }

    public static void Main(string[] args)
    {
        int number = 6;
        Console.WriteLine($"Fibonacci({number}) = {Fibonacci(number)}");  // Çıktı: 8
    }
}
```

**Binary Search Özyinelemeli Fonksiyonu***
```csharp
public static int BinarySearch(int[] arr, int target, int low, int high)
{
    if (low > high)
    {
        return -1; // Base case: eleman bulunamadı
    }
    int mid = (low + high) / 2;
    // Eğer hedef eleman ortadaki eleman ise
    if (arr[mid] == target)
    {
        return mid;
    }
    // Eğer hedef eleman ortadaki elemandan küçükse, sola git
    else if (arr[mid] > target)
    {
        return BinarySearch(arr, target, low, mid - 1);
    }
    // Eğer hedef eleman ortadaki elemandan büyükse, sağa git
    else
    {
        return BinarySearch(arr, target, mid + 1, high);
    }
}
```

---
# Sıralama Algoritmaları

Bu döküman, çeşitli sıralama algoritmalarının çalışma mantıklarını ve C# kod örneklerini içermektedir.

---

## 1. Selection Sort (Seçmeli Sıralama)

### Açıklama
Selection Sort, diziyi sıralamak için en küçük (veya en büyük) elemanı bulup sıralanmamış kısmın başına yerleştirir.

### Nasıl Çalışır?
- Listeyi baştan sona tarar ve en küçük elemanı bulur.
- Bulduğu en küçük elemanı listenin başındaki elemanla yer değiştirir.
- Bu işlemi listenin sıralanmamış kısmı için tekrarlar.

### Zaman Karmaşıklığı:
En iyi, en kötü ve ortalama durum: O(N^2)

### Özellikler:
- Basittir ancak büyük veriler için yavaştır.
- Kararlı bir algoritma değildir.

### C# Kod Örneği
```csharp
void SelectionSort(int[] array)
{
    int n = array.Length;

    for (int i = 0; i < n - 1; i++)
    {
        int minIndex = i;
        for (int j = i + 1; j < n; j++)
        {
            if (array[j] < array[minIndex])
                minIndex = j;
        }
        // Swap
        int temp = array[minIndex];
        array[minIndex] = array[i];
        array[i] = temp;
    }
}
```

---

## 2. Bubble Sort (Kabarcık Sıralama)

### Açıklama
Bubble Sort, bitişik elemanları karşılaştırarak sıralar. Her geçişte en büyük eleman sona taşınır.

### Nasıl Çalışır?
- Listenin bitişik elemanlarını karşılaştırır ve yanlış sıralanmışlarsa yer değiştirir.
- Bu işlemi listenin sonuna kadar tekrarlar ve her geçişte en büyük elemanı sona taşır.
### Zaman Karmaşıklığı:
- En iyi durum: O(N)
- En kötü ve ortalama durum: O(N^2) 

### Özellikler:
Basit bir algoritmadır, eğitim amaçlı kullanılır.
Kararlı bir sıralama algoritmasıdır.

### C# Kod Örneği
```csharp
void BubbleSort(int[] array)
{
    int n = array.Length;
    bool swapped;

    do
    {
        swapped = false;
        for (int i = 0; i < n - 1; i++)
        {
            if (array[i] > array[i + 1])
            {
                // Swap
                int temp = array[i];
                array[i] = array[i + 1];
                array[i + 1] = temp;
                swapped = true;
            }
        }
    } while (swapped);
}
```

---

## 3. Insertion Sort (Ekleme Sıralaması)

### Açıklama
Insertion Sort, dizinin her elemanını sıralanmış alt listeye doğru pozisyona ekler.

### Nasıl Çalışır?
- Her adımda bir elemanı seçer ve onu sıralanmış alt listeye doğru pozisyona ekler.
- Bu işlemi tüm liste sıralanana kadar tekrarlar.
## Zaman Karmaşıklığı:
- En iyi durum: O(N)
- En kötü ve ortalama durum: O(N^2) 
### Özellikler:
- Küçük veri kümelerinde etkilidir.
- Kararlı bir algoritmadır.

### C# Kod Örneği
```csharp
void InsertionSort(int[] array)
{
    int n = array.Length;

    for (int i = 1; i < n; i++)
    {
        int key = array[i];
        int j = i - 1;

        // Move elements of array[0..i-1] that are greater than key
        while (j >= 0 && array[j] > key)
        {
            array[j + 1] = array[j];
            j--;
        }
        array[j + 1] = key;
    }
}
```

---

## 4. Quick Sort (Hızlı Sıralama)

### Açıklama
Quick Sort, bir pivot eleman seçerek diziyi pivotun küçüğüne ve büyüğüne ayırarak sıralar.

### Nasıl Çalışır?
- Bir pivot eleman seçilir.
- Listenin elemanları pivotun küçüğüne ve büyüğüne göre ikiye ayrılır.
- Alt listeler aynı yöntemle tekrar sıralanır.
### Zaman Karmaşıklığı:
- En iyi ve ortalama durum: O(N logN)
- En kötü durum: O(N^2)  (liste ters sıralıysa ve kötü bir pivot seçilirse)

### Özellikler:
- Genellikle en hızlı sıralama yöntemlerinden biridir.
- Kararlı bir algoritma değildir.

### C# Kod Örneği
```csharp
void QuickSort(int[] array, int low, int high)
{
    if (low < high)
    {
        int pi = Partition(array, low, high);
        QuickSort(array, low, pi - 1); // Left partition
        QuickSort(array, pi + 1, high); // Right partition
    }
}

int Partition(int[] array, int low, int high)
{
    int pivot = array[high];
    int i = low - 1;

    for (int j = low; j < high; j++)
    {
        if (array[j] < pivot)
        {
            i++;
            // Swap
            int temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
    }
    // Swap pivot
    int temp1 = array[i + 1];
    array[i + 1] = array[high];
    array[high] = temp1;

    return i + 1;
}
```

---

## 5. Merge Sort (Birleştirme Sıralaması)

### Açıklama
Merge Sort, diziyi sürekli olarak iki alt diziye böler ve alt dizileri sıralayıp birleştirir.

### Nasıl Çalışır?
- Listeyi sürekli olarak iki alt listeye böler.
- Alt listeleri sıralar ve birleştirerek sıralı listeyi oluşturur.
### Zaman Karmaşıklığı:
- Her durumda: O(N logN)
## Özellikler:
- Kararlı bir sıralama algoritmasıdır.
- Daha fazla bellek kullanır (O(N))

### C# Kod Örneği
```csharp
void MergeSort(int[] array, int left, int right)
{
    if (left < right)
    {
        int mid = (left + right) / 2;

        MergeSort(array, left, mid); // Left half
        MergeSort(array, mid + 1, right); // Right half
        Merge(array, left, mid, right); // Merge halves
    }
}

void Merge(int[] array, int left, int mid, int right)
{
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int[] leftArray = new int[n1];
    int[] rightArray = new int[n2];

    for (int i = 0; i < n1; i++) leftArray[i] = array[left + i];
    for (int j = 0; j < n2; j++) rightArray[j] = array[mid + 1 + j];

    int i1 = 0, i2 = 0, k = left;

    while (i1 < n1 && i2 < n2)
    {
        if (leftArray[i1] <= rightArray[i2])
        {
            array[k] = leftArray[i1];
            i1++;
        }
        else
        {
            array[k] = rightArray[i2];
            i2++;
        }
        k++;
    }

    while (i1 < n1) array[k++] = leftArray[i1++];
    while (i2 < n2) array[k++] = rightArray[i2++];
}
```

---

## 6. Radix Sort (Basamak Sıralaması)

### Açıklama
Radix Sort, elemanları basamaklarına göre sıralar (örneğin, birler, onlar basamağı) ve bu işlemi her basamak için tekrarlar.

### Nasıl Çalışır?
- Sayıları basamaklarına göre sıralar (örneğin, birler, onlar, yüzler basamağı).
- Her basamak için sıralama yapılır.
- Sıralama genellikle kararlı bir algoritma (Counting Sort) ile yapılır.
### Zaman Karmaşıklığı:
O(n * k)  burada k en uzun sayının basamak sayısıdır.
### Özellikler:
- Sayılar için etkilidir.
- Kararlı bir algoritmadır.

### C# Kod Örneği
```csharp
void RadixSort(int[] array)
{
    int max = array.Max();
    for (int exp = 1; max / exp > 0; exp *= 10)
        CountSort(array, exp);
}

void CountSort(int[] array, int exp)
{
    int n = array.Length;
    int[] output = new int[n];
    int[] count = new int[10];

    for (int i = 0; i < n; i++)
        count[(array[i] / exp) % 10]++;

    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--)
    {
        output[count[(array[i] / exp) % 10] - 1] = array[i];
        count[(array[i] / exp) % 10]--;
    }

    for (int i = 0; i < n; i++)
        array[i] = output[i];
}
```


---

# Algoritma Karmaşıklığının Hesaplanması ve Algoritma Etkinliği

## Tanım
Algoritma karmaşıklığı, bir algoritmanın çalışma süresi ve kullanılan bellek gibi kaynaklarını belirlemek için kullanılan bir kavramdır. Karmaşıklık, genellikle girdi boyutunun (n) büyüklüğüne bağlı olarak nasıl davrandığını anlamamıza yardımcı olur. Bu sayede, farklı algoritmalar arasında seçim yaparken hangi algoritmanın daha verimli olduğunu anlayabiliriz.

Algoritma etkinliği, bir algoritmanın belirli bir problemi çözme sürecinde en verimli şekilde çalışıp çalışmadığını değerlendirmektir. Etkinlik, genellikle **zaman karmaşıklığı** ve **uzay karmaşıklığı** açısından ölçülür.

## Zaman Karmaşıklığı

Zaman karmaşıklığı, bir algoritmanın çalışmasının, girdi boyutuna göre nasıl değiştiğini ifade eder. Girdi büyüklüğü arttıkça algoritmanın çalışma süresi artar. Zaman karmaşıklığını belirlemek için en yaygın kullanılan notasyonlar şunlardır:

- **O(1)**: Sabit zaman (veya constant time). Algoritmanın çalışma süresi girdi boyutundan bağımsızdır.
- **O(n)**: Lineer zaman (veya linear time). Çalışma süresi girdi boyutuyla doğru orantılıdır.
- **O(n^2)**: Kuadratik zaman (veya quadratic time). Çalışma süresi girdi boyutunun karesiyle orantılıdır.
- **O(log n)**: Logaritmik zaman (veya logarithmic time). Çalışma süresi logaritmik olarak artar, genellikle ikili arama gibi algoritmalarda görülür.
- **O(n log n)**: Lineer-logaritmik zaman. Bu karmaşıklık, sıralama algoritmalarında sıklıkla görülür (örneğin, quicksort ve mergesort).

### Örnek: Zaman Karmaşıklığı Hesaplama

**Algoritma**: Bir diziyi sıralama.

```csharp
public class TimeComplexityExamples
{
    public static void BubbleSort(int[] arr)
    {
        int n = arr.Length;
        for (int i = 0; i < n - 1; i++)  // Dış döngü: O(n)
        {
            for (int j = 0; j < n - i - 1; j++)  // İç döngü: O(n-i)
            {
                if (arr[j] > arr[j + 1])  // Karşılaştırma: O(1)
                {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void Main(string[] args)
    {
        int[] arr = { 64, 34, 25, 12, 22, 11, 90 };
        BubbleSort(arr);
        Console.WriteLine(string.Join(", ", arr));  // Sıralı dizi
    }
}
```

---

# Arama Algoritmaları: Sıralı Arama ve İkili Arama

Arama algoritmaları, bir veri kümesinde belirli bir öğeyi bulmak için kullanılan yöntemlerdir. Bu algoritmalar, genellikle zaman karmaşıklığı açısından değerlendirilir. Bu dokümanda, sıralı arama ve ikili arama algoritmalarını inceleyeceğiz.

## 1. Sıralı Arama (Linear Search)

Sıralı arama, en basit arama algoritmalarından biridir. Bu algoritma, dizinin her öğesini sırayla kontrol eder ve aranan öğe bulunduğunda aramayı sonlandırır. Eğer öğe dizide yoksa, algoritma dizinin sonuna kadar arama yapar ve öğe bulunmaz.

### Zaman Karmaşıklığı
- **En kötü durum**: O(n) - Dizinin her öğesi sırasıyla kontrol edilir.
- **Ortalama durum**: O(n) - Aynı şekilde, öğe ortada veya dizinin sonunda olabilir.
- **En iyi durum**: O(1) - Öğenin ilk sırada bulunması durumunda.

### C# Kod Örneği: Sıralı Arama

```csharp
using System;

public class LinearSearchExample
{
    // Sıralı arama algoritması
    public static int LinearSearch(int[] arr, int target)
    {
        for (int i = 0; i < arr.Length; i++)  // Dizinin her elemanını kontrol et
        {
            if (arr[i] == target)  // Öğeyi bulduğunda
            {
                return i;  // Öğenin bulunduğu indeks döndürülür
            }
        }
        return -1;  // Öğe bulunamazsa -1 döndürülür
    }

    public static void Main(string[] args)
    {
        int[] arr = { 5, 3, 8, 4, 2, 9 };
        int target = 4;
        int result = LinearSearch(arr, target);

        if (result != -1)
            Console.WriteLine($"Öğe {target} bulundu, indeksi: {result}");
        else
            Console.WriteLine("Öğe bulunamadı.");
    }
}
```

# İkili Arama (Binary Search)

İkili arama, sıralı bir dizide öğe aramak için kullanılan etkili bir algoritmadır. Bu algoritma, her adımda arama alanını yarıya indirerek aramayı gerçekleştirir. Bu sayede, büyük veri kümelerinde bile hızlı sonuçlar elde edilebilir.

## İkili Arama Algoritmasının Çalışma Prensibi

1. **Dizi sıralı olmalıdır**: İkili arama, yalnızca sıralı dizilerde çalışır. Eğer dizi sırasızsa, önce sıralama yapılması gerekir.
2. **Başlangıç ve bitiş indekslerini belirleme**: Dizinin başı (`low`) ve sonu (`high`) belirlenir. 
3. **Ortadaki öğeyi kontrol etme**: Dizinin ortasındaki öğe ile aranan öğe karşılaştırılır. 
4. **İki yarıya bölme**:
   - Eğer aranan öğe ortadaki öğeden küçükse, sağ yarıya bakmaya gerek yoktur. Arama sol yarıda devam eder.
   - Eğer aranan öğe ortadaki öğeden büyükse, sol yarıya bakmaya gerek yoktur. Arama sağ yarıda devam eder.
5. **Tekrar etme**: Arama alanı her adımda yarıya düşer. Bu işlem, öğe bulunana kadar veya arama alanı boşalana kadar tekrarlanır.

## Zaman Karmaşıklığı
- **En kötü durum**: O(log n) — Her adımda arama alanı ikiye bölünür.
- **Ortalama durum**: O(log n) — Aynı şekilde, her adımda dizinin boyutu yarıya düşer.
- **En iyi durum**: O(1) — Aranan öğe dizinin ortasında bulunursa.

## İkili Arama'nın Adımları

1. Diziyi sıralayın (gerekiyorsa).
2. Başlangıç (`low`) ve bitiş (`high`) indekslerini belirleyin.
3. Ortadaki öğeyi bulun ve aranan öğe ile karşılaştırın.
4. Arama alanını yarıya bölerek işlemi tekrarlayın.

## C# Kod Örneği: İkili Arama

```csharp
using System;

public class BinarySearchExample
{
    // İkili arama algoritması
    public static int BinarySearch(int[] arr, int target)
    {
        int low = 0;
        int high = arr.Length - 1;

        while (low <= high)
        {
            int mid = low + (high - low) / 2;  // Ortadaki öğe

            if (arr[mid] == target)  // Eğer öğe bulunduysa
                return mid;

            if (arr[mid] < target)  // Aranan öğe sağ yarıda ise
                low = mid + 1;
            else  // Aranan öğe sol yarıda ise
                high = mid - 1;
        }
        return -1;  // Öğe bulunamazsa -1 döndürülür
    }

    public static void Main(string[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int target = 4;
        int result = BinarySearch(arr, target);

        if (result != -1)
            Console.WriteLine($"Öğe {target} bulundu, indeksi: {result}");
        else
            Console.WriteLine("Öğe bulunamadı.");
    }
}
```

### Açıklama
Bu örnekte, BinarySearch fonksiyonu, sıralı bir dizide verilen target öğesini arar. Arama işlemi sırasında, dizinin her seferinde ikiye bölündüğü için zaman karmaşıklığı O(log n) olur. Fonksiyon, öğe bulunduğunda indeksini döndürür, aksi takdirde -1 döndürür.

### Hangi Durumda İkili Arama Kullanılmalı?
Sıralı Diziler: İkili arama, yalnızca sıralı dizilerde çalışır. Eğer dizi sırasızsa, önce sıralama yapılmalıdır.
Büyük Veri Kümeleri: İkili arama, büyük veri kümelerinde daha verimlidir, çünkü her adımda arama alanı yarıya düşer.

---


# Hashing Yöntemleri ve Uygulaması

Hashing, veri yapılarını hızla erişilebilir hale getirmek için kullanılan bir tekniktir. Hashing, bir anahtarın (key) bir dizi veriyle ilişkilendirilmesini sağlar ve bu ilişkileri hızlı bir şekilde aramayı mümkün kılar. Bu, genellikle anahtar-değer çiftlerini saklamak için kullanılır.

## 1. Hashing Nedir?

Hashing, bir anahtarın sabit uzunlukta bir değere dönüştürülmesi işlemidir. Bu sabit uzunluktaki değer, "hash değeri" veya "hash kodu" olarak adlandırılır. Hash fonksiyonu, girdi olarak bir anahtar alır ve buna karşılık gelen hash kodunu üretir.

Hashing'in temel avantajı, veriye hızlı erişim sağlamasıdır. Anahtar, hash fonksiyonu ile bir hash değeri üretildikten sonra, bu hash değeri ile veriye hızlı bir şekilde ulaşılabilir.

### Hash Fonksiyonu

Hash fonksiyonu, bir anahtarı sabit uzunluktaki bir sayıya dönüştüren bir algoritmadır. İyi bir hash fonksiyonu şu özelliklere sahip olmalıdır:
- **Hızlı çalışmalıdır**.
- **Düşük çakışma olasılığına sahip olmalıdır**: Farklı anahtarlar farklı hash kodlarına dönüştürülmelidir.
- **Deterministik olmalıdır**: Aynı anahtar her zaman aynı hash değerini üretmelidir.

## 2. Hash Tablosu

Hashing, verilerin hızlı bir şekilde saklanması ve erişilmesi için genellikle hash tablolarında kullanılır. Hash tablosu, anahtar-değer çiftlerini saklayan bir veri yapısıdır. Anahtar, hash fonksiyonu tarafından dönüştürülerek dizinin bir indeksine karşılık gelir ve değer bu indekse yerleştirilir.

### Hash Tablosunun Yapısı
Hash tablosu, genellikle şu bileşenlerden oluşur:
- **Anahtarlar**: Verinin benzersiz tanımlayıcılarıdır.
- **Hash Fonksiyonu**: Anahtarı, tabloda yer alan bir indekse dönüştürür.
- **Veriler (Değerler)**: Anahtarlara karşılık gelen veriler.

### Hash Tablosunun Avantajları
- **Hızlı Erişim**: Ortalama O(1) zaman karmaşıklığına sahiptir. Yani, veriye doğrudan erişilebilir.
- **Basit Yapı**: Anahtar-değer çiftlerinin saklanması için oldukça verimli ve basit bir yapıdır.

## 3. Hashing Yöntemleri

### 1. Çakışma (Collision) ve Çakışma Yönetimi

Hashing işlemi, farklı anahtarların aynı hash değerine sahip olmasına yol açabilir. Bu duruma **çakışma** (collision) denir. İyi bir hash fonksiyonu, çakışmaların önüne geçmeye çalışır. Ancak, çakışmalar kaçınılmaz olabilir, bu yüzden çakışma yönetimi için çeşitli yöntemler vardır.

#### Çakışma Yönetim Yöntemleri
- **Zincirleme Yöntemi (Chaining)**: Her hash değeri, aynı hash koduna sahip öğeleri tutan bir bağlı liste ile ilişkilendirilir.
- **Açık Adresleme (Open Addressing)**: Eğer bir anahtar çakışma yaşarsa, yeni bir yer aramak için belirli bir strateji izlenir.

### 2. Zincirleme Yöntemi (Chaining)

Zincirleme yöntemi, her hash tablosu hücresinde bir liste veya bağlantılı liste tutarak çakışmaları çözer. Bu yöntem, çakışan öğelerin her birinin bir listeye yerleştirilmesini sağlar.

#### C# Kod Örneği: Zincirleme Yöntemi ile Hashing

```csharp
using System;
using System.Collections.Generic;

public class HashTableChaining
{
    // Hash Tablosu sınıfı
    private List<int>[] table;

    public HashTableChaining(int size)
    {
        table = new List<int>[size];
        for (int i = 0; i < size; i++)
        {
            table[i] = new List<int>();  // Her hücre için bir bağlantılı liste
        }
    }

    // Hash fonksiyonu
    private int Hash(int key)
    {
        return key % table.Length;
    }

    // Anahtar ekleme
    public void Add(int key)
    {
        int index = Hash(key);
        table[index].Add(key);  // Çakışan öğeleri ekler
    }

    // Anahtar arama
    public bool Search(int key)
    {
        int index = Hash(key);
        return table[index].Contains(key);  // Bağlantılı listeyi kontrol eder
    }

    public static void Main()
    {
        HashTableChaining hashTable = new HashTableChaining(5);
        hashTable.Add(10);
        hashTable.Add(15);
        hashTable.Add(20);
        hashTable.Add(25);

        Console.WriteLine(hashTable.Search(15));  // True
        Console.WriteLine(hashTable.Search(30));  // False
    }
}
```

### 3. Açık Adresleme Yöntemi (Open Addressing)
Açık adresleme, çakışma yaşandığında, yeni bir yer aramak için belirli bir strateji kullanır:

- Doğrudan Arama (Linear Probing): Eğer bir hücre doluysa, bir sonraki hücreye bakılır.
- Kuadratik Arama (Quadratic Probing): Eğer bir hücre doluysa, arama adımı kuadratik bir artışla yapılır.
- Çift Hashing (Double Hashing): Birden fazla hash fonksiyonu kullanılarak yeni bir yer bulunur.

### 4. Hashing Uygulamaları
1.  Veri Tabanı Yönetim Sistemleri
Hashing, veritabanlarında hızlı veri erişimi sağlamak için kullanılır. SQL veritabanlarında indeksleme için hash tablosu kullanılabilir.

2. Kriptografi
Hashing, şifreleme ve dijital imza işlemlerinde, verilerin doğruluğunu ve bütünlüğünü sağlamak için yaygın olarak kullanılır.

3. Dosya Eşleştirme
Dosya sistemlerinde dosya adlarının benzersizliğini sağlamak ve veriye hızlı erişim sağlamak için hashing kullanılabilir.

4. Veri Yapılarında Arama
Hashing, verilerin hızlı bir şekilde aranması gereken veri yapılarında, özellikle hash tablolarında yaygın olarak kullanılır.

---

# Ağaç Yapıları ve İkili Ağaçlar

Ağaç veri yapısı, hiyerarşik bir yapıyı temsil etmek için kullanılan, düğümler (nodes) ve bu düğümler arasında bağlantılar (kenarlar) bulunan bir veri yapısıdır. Ağaçlar, özellikle veri depolama, sıralama, arama ve daha pek çok alanda kullanılır. Ağaç yapısının temel özelliklerinden biri, her düğümün sadece bir ebeveyn (parent) düğümü olabilmesidir.

## 1. Ağaç Yapısının Temel Bileşenleri

Ağaç yapısının temel bileşenleri şunlardır:
- **Kök Düğüm (Root)**: Ağacın başlangıç düğümüdür ve tüm diğer düğümler bu düğümden türetilir.
- **Yaprak Düğüm (Leaf)**: Alt düğümü olmayan düğümlerdir.
- **İç Düğüm (Internal Node)**: Hem ebeveyn hem de çocuk düğümleri olan düğümlerdir.
- **Kardeş Düğüm (Sibling)**: Aynı ebeveyni paylaşan düğümlerdir.
- **Düğüm Derinliği (Node Depth)**: Bir düğümün kök düğümünden olan uzaklığıdır.
- **Ağaç Yüksekliği (Tree Height)**: Ağacın en uzun yolunun uzunluğudur.

## 2. İkili Ağaçlar

İkili ağaç, her düğümün en fazla iki çocuğa sahip olabileceği bir ağaç yapısıdır. İkili ağaçlar genellikle **ikili arama ağaçları (binary search trees)**, **ikili yığınlar (binary heaps)** ve **ikili denge ağaçları (AVL, Red-Black trees)** gibi uygulamalarda kullanılır.

### 2.1. İkili Ağaçların Özellikleri

- Her düğüm, bir **sol çocuk** ve bir **sağ çocuk** düğümüne sahip olabilir.
- Her düğümün bir **anahtar değeri** vardır.
- Kök düğümden başlayarak, her düğümün sol alt ağacındaki tüm anahtarlar, o düğümün anahtarından küçük ve sağ alt ağacındaki tüm anahtarlar o düğümün anahtarından büyük olacak şekilde sıralıdır (ikili arama ağacı için geçerlidir).

### 2.2. İkili Ağaçların Tipleri

- **İkili Arama Ağacı (Binary Search Tree - BST)**: Her düğümün sol alt ağacındaki tüm düğümlerin değeri, o düğümün değerinden küçük ve sağ alt ağacındaki tüm düğümlerin değeri, o düğümün değerinden büyüktür.
  
- **İkili Yığın (Binary Heap)**: Genellikle öncelikli kuyruğun uygulanmasında kullanılır. İki ana türü vardır:
  - **Max-Heap**: Kök düğüm en büyük öğeyi tutar.
  - **Min-Heap**: Kök düğüm en küçük öğeyi tutar.
  
- **AVL Ağacı (AVL Tree)**: İkili arama ağacının bir türüdür ve dengede kalması için her düğümün sol ve sağ alt ağaçlarının yükseklik farkı -1, 0 veya +1 olmalıdır.

- **Red-Black Tree**: Dengeli bir ikili arama ağacı türüdür. Her düğümde renk (kırmızı veya siyah) bulunur ve bu renkler, ağacın dengede kalmasına yardımcı olur.

## 3. İkili Ağaçlarda Temel İşlemler

İkili ağaçlar üzerinde bazı temel işlemler aşağıdaki gibidir:

### 3.1. Ekleme (Insert)
Bir düğüm eklerken, uygun pozisyonu bulmak için ağacın yapısını takip ederiz. İkili arama ağacında, yeni düğümün değeri, mevcut düğümün değerinden küçükse sol alt ağaca, büyükse sağ alt ağaca yerleştirilir.

#### C# Kod Örneği: İkili Ağaçta Ekleme

```csharp
public class BinaryTree
{
    public class Node
    {
        public int Value;
        public Node Left;
        public Node Right;

        public Node(int value)
        {
            Value = value;
            Left = null;
            Right = null;
        }
    }

    public Node Root;

    public BinaryTree()
    {
        Root = null;
    }

    // Ekleme işlemi
    public void Insert(int value)
    {
        Root = InsertRec(Root, value);
    }

    // Rekürsif ekleme
    private Node InsertRec(Node root, int value)
    {
        // Eğer kök boşsa, yeni düğüm eklenir
        if (root == null)
        {
            root = new Node(value);
            return root;
        }

        // Değer küçükse sol alt ağaçta yerleştirilir
        if (value < root.Value)
        {
            root.Left = InsertRec(root.Left, value);
        }
        // Değer büyükse sağ alt ağaçta yerleştirilir
        else if (value > root.Value)
        {
            root.Right = InsertRec(root.Right, value);
        }

        return root;
    }
}
```
## 3.2. Arama (Search)
Bir ikili ağaçta arama yapmak için, istenen değeri bulana kadar ağaç boyunca geziniriz. Eğer aradığımız değer küçükse, sol alt ağaçta, büyükse sağ alt ağaçta aramaya devam ederiz.
```csharp
public bool Search(int value)
{
    return SearchRec(Root, value);
}

private bool SearchRec(Node root, int value)
{
    // Eğer kök boşsa, değer bulunamamıştır
    if (root == null)
    {
        return false;
    }

    // Değer bulunduysa
    if (root.Value == value)
    {
        return true;
    }

    // Değer küçükse sol alt ağaçta arama yapılır
    if (value < root.Value)
    {
        return SearchRec(root.Left, value);
    }
    // Değer büyükse sağ alt ağaçta arama yapılır
    return SearchRec(root.Right, value);
}
```

### 3.3. Silme (Delete)
İkili ağaçlarda silme işlemi, üç farklı durumu kapsar:
- Düğümün hiçbir çocuğu yoksa (yaprak düğüm).
- Düğümün bir çocuğu varsa.
- Düğümün iki çocuğu varsa.

İkinci ve üçüncü durumlar için ek stratejiler gereklidir.

## 4. İkili Ağaçların Uygulamaları
### 4.1. Veri Yapılarında Arama
İkili arama ağaçları, verileri sıralı şekilde depolayarak hızlı arama, ekleme ve silme işlemleri sağlar. Bu ağaçlar, veritabanlarında ve dosya sistemlerinde yaygın olarak kullanılır.

### 4.2. İfadelerin Sıralanması
İkili ağaçlar, özellikle infix, prefix ve postfix gösterimlerinin dönüşümünde kullanılır. İfadenin analiz edilmesinde bu tür ağaç yapıları çok faydalıdır.

### 4.3. Hızlı En Küçük ve En Büyük Eleman
İkili arama ağaçları, en küçük ve en büyük elemanları bulmayı hızlı bir şekilde sağlar. Bu işlem, ağacın sol veya sağ en alt yaprak düğümüne gitmekle yapılabilir.

## 5. Sonuç
İkili ağaçlar, verilerin sıralanması, hızlı arama yapılması ve veri üzerinde düzenli işlemler yapılması için oldukça faydalı bir veri yapısıdır. İkili arama ağacının dengeli olması, işlem verimliliğini artırır ve daha hızlı erişim sağlar. Bu nedenle, veri yapılarının performansını optimize etmek için ikili ağaçlar sıklıkla kullanılır.

---


# Graf Yapıları, Yönlü Graflar ve Graf Algoritmaları

Graf veri yapısı, düğümler (vertices) ve bu düğümler arasındaki bağlantılardan (edges) oluşan bir yapıdır. Graf yapıları, çeşitli ilişkileri modellemek için yaygın olarak kullanılır. Örneğin, sosyal ağlar, yol haritaları, bilgisayar ağları ve yönlendirilmiş iş akışları gibi pek çok uygulamada graf yapıları kullanılır.

## 1. Graf Yapısının Temel Bileşenleri

Bir grafın temel bileşenleri şunlardır:
- **Düğüm (Vertex)**: Grafın temel elemanıdır ve üzerinde işlem yapılan öğedir. Düğüm, bir varlık veya obje olabilir.
- **Bağlantı (Edge)**: İki düğüm arasındaki ilişkidir. Bir bağlantı, yönlü veya yönsüz olabilir.
  - **Yönlü Bağlantı (Directed Edge)**: Bağlantının bir yönü vardır. Bu, bir düğümden diğerine doğru bir akış olduğunu ifade eder.
  - **Yönsüz Bağlantı (Undirected Edge)**: Bağlantı her iki yönde de geçerlidir.
  
Graf yapısındaki düğümler ve bağlantılar arasında bazı ilişki türleri bulunabilir:
- **Komşuluk (Adjacency)**: Bir düğümün doğrudan bağlı olduğu düğümlerdir.
- **Derece (Degree)**: Bir düğümün sahip olduğu bağlantı sayısıdır.
  - **İçe Derece (In-degree)**: Bir düğüme yönlendirilmiş olan bağlantıların sayısı (yönlü graf için geçerlidir).
  - **Dışa Derece (Out-degree)**: Bir düğümden çıkan bağlantıların sayısı (yönlü graf için geçerlidir).

## 2. Yönlü Graflar

Yönlü graf (directed graph veya digraph), her bağlantının bir başlangıç ve bitiş noktası (başlangıç ve hedef düğüm) olduğu bir graf türüdür. Yönlü graf, bir düğümden başka bir düğüme giden tek yönlü bir ilişkiyi temsil eder.

### 2.1. Yönlü Grafın Özellikleri
- **Düğüm ve Yönlü Bağlantılar**: Yönlü bir graf, her bağlantının bir yönü olduğu için, bağlantıların başlangıç ve bitiş noktaları net bir şekilde tanımlanır.
- **Dönüşüm (Cycle)**: Yönlü bir graf, bir düğümden başlayıp geri kendisine dönebilen bir yol içeriyorsa bu yol bir dönüşüm (cycle) oluşturur.
  
### 2.2. Yönlü Graf Türleri
- **Ağaç (Tree)**: Yönlü grafın bir türüdür ve döngüsüzdür. Ağaçlar, hiyerarşik yapıları modellemek için yaygın kullanılır.
- **Ağ Yönlü Graf (Flow Network)**: Bu tür yönlü graf, genellikle taşıma problemlerini çözmek için kullanılır, örneğin, ağlarda veri iletimi veya boru hatlarında sıvı taşınması.

## 3. Graf Algoritmaları

Graf teorisi, ağların ve ilişkilerin modellenmesinin yanı sıra, bu graf üzerinde çeşitli işlemleri gerçekleştirebilmek için algoritmalar sunar. En yaygın graf algoritmalarından bazıları şunlardır:

### 3.1. Derinlik Öncelikli Arama (Depth-First Search - DFS)
Derinlik öncelikli arama, bir grafın tüm düğümlerini ziyaret etmek için kullanılan bir algoritmadır. Bu algoritma, her düğümün komşularını ziyaret ettikten sonra geri dönerek derinlemesine bir arama gerçekleştirir.

#### DFS Algoritması Adımları
1. Başlangıç düğümünü işaretle ve komşusuna git.
2. Komşu düğümdeki komşulara git.
3. Her düğüm ziyaret edilirken geri dönüp, önceki düğümün diğer komşularına geçilir.

#### C# Kod Örneği: Derinlik Öncelikli Arama

```csharp
public class Graph
{
    private Dictionary<int, List<int>> adjacencyList;

    public Graph()
    {
        adjacencyList = new Dictionary<int, List<int>>();
    }

    // Grafın düğümleri arasında bağlantı ekleme
    public void AddEdge(int start, int end)
    {
        if (!adjacencyList.ContainsKey(start))
        {
            adjacencyList[start] = new List<int>();
        }
        adjacencyList[start].Add(end);
    }

    // Derinlik öncelikli arama (DFS)
    public void DFS(int start)
    {
        var visited = new HashSet<int>();
        DFSRecursive(start, visited);
    }

    private void DFSRecursive(int node, HashSet<int> visited)
    {
        if (visited.Contains(node))
        {
            return;
        }

        visited.Add(node);
        Console.WriteLine(node); // Ziyaret edilen düğüm

        // Komşuları ziyaret et
        foreach (var neighbor in adjacencyList[node])
        {
            DFSRecursive(neighbor, visited);
        }
    }
}
```

### 3.2. Genişlik Öncelikli Arama (Breadth-First Search - BFS)
Genişlik öncelikli arama, bir grafın tüm düğümlerini katmanlar halinde ziyaret eder. Başlangıç düğümünden komşuları ilk olarak ziyaret edilir ve daha sonra daha uzak komşulara geçilir.

**BFS Algoritması Adımları**
- Başlangıç düğümünü kuyruğa ekle.
- Kuyruk boşalana kadar:
- Kuyruğun önündeki düğümü çıkar.
- Komşularını kuyruğa ekle.
- Düğüm her zaman ilk sırada işaretlenir.

**C# Kod Örneği: Genişlik Öncelikli Arama**
```csharp
public void BFS(int start)
{
    var visited = new HashSet<int>();
    var queue = new Queue<int>();

    visited.Add(start);
    queue.Enqueue(start);

    while (queue.Count > 0)
    {
        var node = queue.Dequeue();
        Console.WriteLine(node); // Ziyaret edilen düğüm

        foreach (var neighbor in adjacencyList[node])
        {
            if (!visited.Contains(neighbor))
            {
                visited.Add(neighbor);
                queue.Enqueue(neighbor);
            }
        }
    }
}
```

### 3.3. Dijkstra Algoritması
Dijkstra algoritması, grafın kaynak düğümünden diğer tüm düğümlere olan en kısa yolu bulmak için kullanılır. Bu algoritma, pozitif ağırlıklı yönlü grafikte uygulanabilir.

**Dijkstra Algoritması Adımları**
- Başlangıç düğümüne en küçük mesafeyi atayın (başlangıçta sıfır).
- Diğer tüm düğümlere sonsuz mesafe atayın.
- En küçük mesafeye sahip düğümü seçin ve komşularına mesafelerini güncelleyin.

### C# Kod Örneği: Dijkstra Algoritması
```csharp
public Dictionary<int, int> Dijkstra(int start)
{
    var distances = new Dictionary<int, int>();
    var priorityQueue = new SortedList<int, int>();

    foreach (var node in adjacencyList.Keys)
    {
        distances[node] = int.MaxValue;
        priorityQueue.Add(node, distances[node]);
    }

    distances[start] = 0;
    priorityQueue[start] = 0;

    while (priorityQueue.Count > 0)
    {
        var currentNode = priorityQueue.First().Key;
        priorityQueue.RemoveAt(0);

        foreach (var neighbor in adjacencyList[currentNode])
        {
            var newDist = distances[currentNode] + 1; // Varsayalım ki her kenar ağırlığı 1

            if (newDist < distances[neighbor])
            {
                distances[neighbor] = newDist;
                priorityQueue[neighbor] = newDist;
            }
        }
    }

    return distances;
}
```

## 4. Graf Uygulamaları
Graf yapıları, pek çok farklı uygulama alanına sahiptir. Bunlardan bazıları şunlardır:

- Sosyal Ağlar: Kullanıcılar arasındaki bağlantıları temsil etmek için kullanılabilir.
- Navigasyon Sistemleri: Yol haritalarında, yolları ve şehirleri temsil etmek için kullanılır.
- Ağ Trafik Yönetimi: Bilgisayar ağlarında veri iletimi ve yönlendirilmesi için kullanılır.
- Kaynak Akışı Problemleri: Akış ağlarında en verimli yolları bulmak için kullanılabilir.
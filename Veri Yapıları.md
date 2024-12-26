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

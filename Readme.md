# TheCashier
Membuat aplikasi kasir dimana Aplikasi ini mencakup perhitungan penjumlahan dan perkalian untuk menghitung harga barang yang akan di beli maupun jasa, barang atau jasa yang sudah di inputkan dan sudah di jumlahkan maupun di kalikan akan masuk pada data list.

## Scope & Functionalities
- User dapat menginputkan huruf/angka
- User dapat menyentuh tombol opsi pilihan barang/jasa
- User dapat menambahkan barang/jasa
- User dapat melihat data list yang sudah di inputkan

## How Does it Works

### Class Item
Setelah pendeklarasian pada class item, dilanjutkan dengan penginisialisasian seluruh bahan sebagai media yang nantinya akan menjadi perwakilan dari variable yang akan diinputkan oleh pengguna.
```csharp
        public Item(int id, string title, int quantity, double price, double subtotal, string type)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.price = price;
            this.subtotal = subtotal;
            this.type = type;
        }
```
Selanjutnya semua bahan akan di buatkan semacam variable perwakilan untuk input. Dibawah ini, terjadi proses dimana nilai dari subtotal diambil dari perkalian nilai price dengan quantity yang selanjutnya akan mewakili getSubtotal()
```csharp
        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
```
### Class Calculator
Dibawah ini berfungsi sebagai penginisialisasian data dari input akan dimasukan dalam satu list yaitu listItem, serta penambahan nilai dari total jika item baru diinputkan ke dalam list secara otomatis
```csharp
        private List<Item> listItem;
        private double total = 0;

        public Calculator()
        {
            this.listItem = new List<Item>();
        }
        public void addItem (Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
```
Lalu berpindah ke MainWindow.xaml.cs sebagai pusat dari semua proses. Dimulai dari pengambilan seluruh bahan-bahan yang digunakan, seperti listItem
```csharp
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }
```
Dan akhir proses dari aplikasi TheCashier ini ada pada coding berikut.
```csharp
        private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, price, price, type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = String.Format("Rp. {0}", total);

            listBox.Items.Refresh();
        }
```
Dimana setelah semua input sudah terbaca, lalu diproses dan di output kan dengan cara ditampilkan dalam listItem dan label yang berada pada sudut bawah. Label tersebut menunjukan total dari seluruh item yang di input kan berserta total harga dan keterangan lainnya.

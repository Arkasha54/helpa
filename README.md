# Мои гайды
## Вставление картинки
```
UPDATE Users SET [image] =
(SELECT * FROM OPENROWSET(BULK N'C:\Users\nasik\Pictures\ff961525.jpg', SINGLE_BLOB) AS image)WHERE ID = 1
```

## Класс менеджера для навигации в фрейме 
```
public static Frame MainFrame { get; set; }

MainFrame.Navigate(new Propiska(null));
```

## Авторизация
```
if (log.Length < 1)
{
  MessageBox.Show("Введите логин!");
}
else
{
if (pas.Length < 1)
{
  MessageBox.Show("Введите пароль!");
}
else
{
   users user = null;
   user = cont.users.Where(u => u.loginn == log & u.passwordd == pas).FirstOrDefault();
   if (user != null)
{
  var main = new GuestCreation();
  this.Close();
  main.Show();
}
else
{
MessageBox.Show("Логин или пароль введены неверно!");
      }
   }
}
```

## Сохранение
```
 if (tbxDomProp.Text != null & tbxStreetProp.Text != null & cmbGorodprop.SelectedItem != null)
            {
                прописка data1 = new прописка();
                var temp = cont.город.ToList().Where(c => c.наименование == cmbGorodprop.Text.ToString()).FirstOrDefault();
                data1.ид_города = temp.ид_города;
                data1.улица = tbxStreetProp.Text;
                data1.номер_дома = tbxDomProp.Text;
                data1.номер_квартиры = Convert.ToInt32(tbxKvarNumProp.Text);
                cont.прописка.Add(data1);
                cont.SaveChanges();
                MessageBox.Show("Прописка добавлена, можете переходить к следующему шагу");
            }
            else 
            {
                MessageBox.Show("Вы не заполнили поля");
            }
```

## Поиск 
```
 cmbGorodprop.ItemsSource = cont.город.Where(x => x.наименование.ToString().Contains(tbxPodrazPosik.Text)).ToList();
            if (tbxPodrazPosik.Text == "")
            {
                cmbGorodprop.ItemsSource = cont.город.ToList();
            }
```

## удаление
```
 var row = dataGrid.SelectedItem as посетитель;
            if (row == null)
            {
                MessageBox.Show("Не выбран элемент");
                return;
            }
            MessageBoxResult result = MessageBox.Show("Вы точно хотите удалить", "удалить", MessageBoxButton.YesNo, MessageBoxImage.Question);
            if (result == MessageBoxResult.Yes)
            {
                cont.посетитель.Remove(row);
                cont.SaveChanges();
                MessageBox.Show("Строка удалилась");
                dataGrid.ItemsSource = cont.посетитель.ToList();
            }
```

## изменение
```
var row = dataGrid.SelectedItem as посетитель;
            if (row == null)
            {
                MessageBox.Show("Не выбран элемент");
                return;
            }
            NavigationService.Navigate(new GostItog(row));
```
ps. окно должно принимать 
```
 public GostItog(посетитель pos)
        {
            InitializeComponent();
            DataContext = pos;
```

# Джулфиковские гайды
## Учитывать регистр в таблице
```
ALTER TABLE AuthAcc 
ALTER COLUMN PasswordAcc nvarchar(20) 
COLLATE SQL_Latin1_General_CP1_CS_AS
```

## DataGrid
```
 <DataGrid.Columns>
     <DataGridTextColumn Header="Id" Binding="{Binding IdUser}"/>
       <DataGridTextColumn Header="role" Binding="{Binding UserRole.RoleName}"/>
```

## Отображение данных из бд
```
SqlCommand cmd = new SqlCommand("select * from TestTable", con);
DataTable dt = new DataTable();
SqlDataAdapter adapter = new SqlDataAdapter(cmd);
adapter.Fill(dt);
DT.ItemsSource = dt.DefaultView;
or
Users_DT.ItemsSource = AppConnect.modelOdb.UserInfo.ToList();
```

## del data
```
delete UserInfo where IdUser between 7 and 7
DataRowView drv = (DataRowView)DT.SelectedItem;
```

## update data
```
 SqlCommand cmd = new SqlCommand($"update TestTable set Descr='{TXB.Text}' where Id={_id}", conn);
 cmd.ExecuteNonQuery();
```

 ## insert data 
 ```
 SqlCommand Com(string cmdText)
{
    SqlCommand cmd = new SqlCommand(cmdText, Connection());
    cmd.ExecuteNonQuery();
    return cmd;
}
 Com($"insert into TestTable (Descr) values ('{Descr_TXB.Text}')");
```
 ## search data
  ```
DataTable dt = new DataTable();
var cmd = Com($"select * from TestTable where Descr LIKE '{Search_TXB.Text}%'");
SqlDataAdapter adapter = new SqlDataAdapter(cmd);
adapter.Fill(dt);
DT.ItemsSource = dt.DefaultView;
```
## Add data to combobox
```
SqlCommand cmd = new SqlCommand("select * from UserRole", conn);
SqlDataReader sqlDataReader = cmd.ExecuteReader();
string RoleN;
while (sqlDataReader.Read())
{
    RoleN = Convert.ToString(sqlDataReader.GetValue(1));
    Role_CMB.Items.Add($"{RoleN}");

}
```

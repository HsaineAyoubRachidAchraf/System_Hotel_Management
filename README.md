<h1 align="center">System Hotel Management</h1>
<p align="center"> <img src="mainwindow.png" title="System Hotel Management "><br> System Hotel Management</p>


<h1 align="center">Introduction</h1>

As part of our first year in engineering, specializing in robotics and cobotics at the School of Digital Engineering and Artificial Intelligence at the euromed University of Fez, our professor proposed to us to create an application as a final project after we are finished the course of human-machine interaction using **QT designer c++**.

<h1 align="center">Thankfulness</h1>

First of all, to begin this report, we would like to express our thanks to
our professor.***Belcaid Anass*** who has not stopped encouraging us during the
duration of the project, as well as its generosity in terms of training and supervision,
for the quality of his exceptional coaching, his patience, his rigour and his
availability during our preparation of this project.
We would like to thank my team who contributed to the success of our project
tutor who helped us a lot in the development of our project.

<h1 align="center">About Application</h1>

System Hotel Management is an appliaction created by **Qt Creator using C++**,is an application allow clients to check the available of rooms then you can book a room available,after this operation we will show your id_number that is mean your number as client in our service when you click on **Transaction Button**,finnally when you want to leave the hotel just check out for make the room available for other client.

<h1 align="center">Steps To use Application</h1>

First of all ou should to do it to go the menu bar:
1. click on **BARAHA HOTEL** then**About Hotel** to show information about our services.
2. click on **Price** to know the price of each room category.
3.  Check the availibilty of the rooms.
4.  Now, we move to button**roombooking**,click on it, fill in the form and click on **sumbit**to valid the reservation.
5.  If you wnt to know your id as client,you should click on **trasaction**.
6.  Know you can quit the application,go to menu bar, click on **BARAHA HOTEL** then**Exit**
7.  When you want to check out the hotel,go to**Button: check out** and choose the number of room selected in your reservation, check out and automaticaly you will quit the application.
8.  We hope you had a good time. 



<h1 align="center">How Application is built?</h1>

1. Our application contain five forms,each one have a specific task to do,the first one is the **mainwindow.ui**:Is the principle form, it contain:menubar,toolbar,Qaction,PushButtons,picture of hotel,calendar...you will find in the table bellow details of forms that remain:

| Form        | Execution   | Description   |
| :---        |    :----:   | :---          |
| bookroomdialog.ui      | <p> <img src="roombook.png" title="Roombooking"></p>       | This form contain a dialog that client should fill in when he/she click on **room booking** after checking the availibillity of rooms,you should be select a room and put all information.<br>it contain labels,combobox,lineedit,two pushbutton and verticalspacer   |
| transaction.ui   | <p> <img src="transaction.png" title="Transaction"></p>        | This form contain label and a listwidget that show the id of client and and the numer of room selected       |
| chechoutdialog.ui   | <p> <img src="chechout.png" title="Check out"></p>          | This form is a dialog contain a combobox,label and pushbutton to valid your check out      |
| roomavailabledialog.ui   | <p> <img src="available.png" title="Available"></p>          | This form is a dialog contain labels for number of rooms and agroupbox gather this labels       |


2. The **menubar** contain **tree menu**each one have two **QAcion**,the first one**BARAHA Hotel**,the first action display information about the hotel,the second to quit the application,the second one **Price** the both action display the price,the last one **Help** hive you inforamation about QT and the application.
3. Each Action have an icon and eachdailog have as well an icon.
4. THe size of all foems is fixed.
5. The toolbar contain all icons of the actions.
6. We are trying to use maximum concepts and tools in this course.
7. The application is built using **MVC Model** especially SQLDATABASE.is responsible for managing of database .
8. Also we are using **Item Based** especially Listwidget in the form transaction.

<h2 align="center">Code source</h2>
You will find our code 
<details>
<summary>Headers</summary>
<br>
  
<details>
<summary>bookroomdialog.h</summary>
<br>
 
```
#ifndef BOOKROOMDIALOG_H
#define BOOKROOMDIALOG_H
#include <QDialog>
#include <QtDebug>
#include <QSqlDatabase>
#include <QSqlDriver>
#include <QSqlError>
#include <QSqlQuery>
#include <QFile>
#include <vector>
#include <QMessageBox>

#include "hotel.h"

namespace Ui {
class BookRoomDialog;
}

class BookRoomDialog : public QDialog
{
    Q_OBJECT

public:
    explicit BookRoomDialog(QWidget *parent = nullptr);
    ~BookRoomDialog();
    void readData();

    QString getname()const;
    int combobox()const;
    QString getaddres()const;
    QString getphone()const; 

private slots:
    void on_btnCancel_clicked();
    void on_btnSubmit_clicked();

private:
    Ui::BookRoomDialog *ui;

};

#endif // BOOKROOMDIALOG_H

```
</details>

<details>
<summary>checkoutdialog.h</summary>
<br>
 
```
#ifndef CHECKOUTDIALOG_H
#define CHECKOUTDIALOG_H

#include <QDialog>
#include <QDebug>
#include <QSqlQuery>
#include <QFile>
#include <QSqlDatabase>
#include <QSqlError>
#include <hotel.h>
#include <QMessageBox>

namespace Ui {
class CheckOutDialog;
}

class CheckOutDialog : public QDialog
{
    Q_OBJECT

public:
    explicit CheckOutDialog(QWidget *parent = nullptr);
    ~CheckOutDialog();
    void readData();
    //int box()const;


private slots:
    void on_btnCancel_clicked();
    void on_btnCheckout_clicked();
private:
    Ui::CheckOutDialog *ui;
};

#endif // CHECKOUTDIALOG_H
 
```
</details>
  
  
<details>
<summary>roomavailabledailog.h></summary>
<br>
 
```
#ifndef ROOMAVAILABLEWINDOW_H
#define ROOMAVAILABLEWINDOW_H
#include <QDialog>
#include <QDebug>
#include <hotel.h>

namespace Ui {
class RoomAvailableDialog;
}

class RoomAvailableDialog : public QDialog
{
    Q_OBJECT

public:
    explicit RoomAvailableDialog(QWidget *parent = nullptr);
    ~RoomAvailableDialog();
    void readData();

    QString groupBox()const;
private slots:
    void on_pushButton_clicked();

private:
    Ui::RoomAvailableDialog *ui;
};
#endif // ROOMAVAILABLEWINDOW_H
 
```
</details> 
  
<details>
<summary>transaction.h</summary>
<br>
 
```
#ifndef TRANSACTION_H
#define TRANSACTION_H
#include <QSqlDatabase>
#include <QSqlDriver>
#include <QSqlError>
#include <QSqlQuery>
#include <QFile>
#include <QDebug>
#include <QSqlTableModel>
#include <QDialog>

namespace Ui {
class transaction;
}

class transaction : public QDialog
{
    Q_OBJECT

public:
    explicit transaction(QWidget *parent = nullptr);
    void readData();
    ~transaction();

private:
    Ui::transaction *ui;
};
#endif // TRANSACTION_H
 
```
</details> 
  
  
<details>
<summary>hotel.h</summary>
<br>
 
```
#ifndef HOTEL_H
#define HOTEL_H

#include <QDialog>
#include <QDebug>
#include <QSqlQuery>
#include <QFile>
#include <QSqlDatabase>
#include <QSqlError>
#include<vector>

class Hotel
{
private:
    Hotel(){}
    Hotel(Hotel const &){}
    static Hotel * instance;
    void updateHotelData(int room); //update DB & Vector

public:
    int BookRoom(int roomno, QString name, QString contactno, QString govid, QString address);
    int CheckOut(int roomno);
    std::vector<int> RoomAvailability();
    std::vector<int> getRoomList(QString);  //return vector
    static Hotel* getInstance();

};

#endif // HOTEL_H
 
```
</details> 
  
<details>
<summary>mainwindow.h</summary>
<br>
 
```
#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include "bookroomdialog.h"
#include "checkoutdialog.h"
#include "roomavailabledialog.h"
#include "transaction.h"

namespace Ui {
class MainWindow;
}

class MainWindow : public QMainWindow
{
    Q_OBJECT

private:
    RoomAvailableDialog * ptrRoomAvailableDlg;
    CheckOutDialog * ptrCheckOutDlg;
    BookRoomDialog * ptrRoomBookingDlg;
    transaction * ptrTransaction;

public:
    explicit MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private slots:
    void on_btnRoomBooking_clicked();
    void on_btnRoomCheckout_clicked();
    void on_btnCheckAvailability_clicked();
    void on_bntTransaction_clicked();
    void on_actionAbout_Application_triggered();

    void on_actionAbout_QT_triggered();

    void on_actionInformation_BARAHA_Hotel_triggered();

    void on_actionExit_triggered();

    void on_actionSingle_room_triggered();

    void on_actionDouble_room_triggered();

private:
    Ui::MainWindow *ui;
};

#endif // MAINWINDOW_H
 
```
</details> 
  
</details>

<details>
<summary>Sources</summary>
<br>
 
<details>
<summary>bookroomdialog.cpp</summary>
<br>
 
```
  
```
</details>

  
<details>
<summary>checkoutdialog.cpp</summary>
<br>
 
```
  
```
</details>
  
<details>
<summaryroomavailabledialog.cpp></summary>
<br>
 
```
  
```
</details> 
  
<details>
<summary>transaction.cpp</summary>
<br>
 
```
  
```
</details>  
  
<details>
<summary>hotel.cpp</summary>
<br>
 
```
  
```
</details>  
  
  
<details>
<summary>mainwindow.cpp</summary>
<br>
 
```
  
```
</details>   
  
 
<details>
<summary>main.cpp</summary>
<br>
 
```
  
```
</details>    
  
</details>


<details>
<summary>Forms</summary>
<br>
 
```
  
```
</details>

<h2 align="center">Compilation</h2>

https://user-images.githubusercontent.com/93345744/152611308-d8e4f65a-4ef6-4ca6-baa7-7d41b1cbfbc7.mp4




https://user-images.githubusercontent.com/93345744/152612941-2dcb4d6d-80e6-464c-801b-64d4f34379b4.mp4




<h1 align="center">Conclusion</h1>

<h1 align="center">Contact</h1>

ayoub.hsaine@eidia.ueuromed.org

achraf.rachid@eidia.ueuromed.org

achraf.berriane@eidia.ueuromed.org



















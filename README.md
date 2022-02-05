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
#include "bookroomdialog.h"
#include "ui_bookroomdialog.h"

BookRoomDialog::BookRoomDialog(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::BookRoomDialog)
{
    ui->setupUi(this);
    this->setWindowTitle("Booking a room");
    this->setFixedSize(500,500);
    this->setWindowIcon(QIcon(":/booking_room.jpg"));

}

void BookRoomDialog:: readData()
{
    qDebug()<<"BookRoomDialog:readData";
    std::vector<int>rooms = Hotel::getInstance()->getRoomList("y");
    this->ui->cmbRoomList->clear();

    for(std::vector<int>::iterator it = rooms.begin(); it!=rooms.end(); it++ )
    {
        this->ui->cmbRoomList->addItem(QString::number(*it));
    }
}

BookRoomDialog::~BookRoomDialog()
{
    delete ui;
}

void BookRoomDialog::on_btnCancel_clicked()
{
    this->hide();
}

void BookRoomDialog::on_btnSubmit_clicked()
{
    //call hotel's book room
    int  roomno = ui->cmbRoomList->currentText().toInt();
    QString name = ui->txtName->text();
    QString contactno = ui->txtContactNumber->text();
    QString address = ui->txtAddress->toPlainText();
    QString govtid = ui->txtIdProof->text();


  //  query.prepare("insert into cppbuzz_customer (name, mobileno, govtid, address) values ('" + name + "','" + contactno + "','" + govtid + "','" + address + "')");


    if(roomno < 1)
    {
            QMessageBox::information(
            this,
            tr("Warning!"),
            tr("We are sold out. No room is available") );
            return;
     }

    int ret = Hotel::getInstance()->BookRoom(roomno, name, contactno, govtid, address);

    QString msg = "";
    ret==0?msg="Success!":"Failure!";

    this->hide();

    if(ret == 0)
    {
        QMessageBox::information(
        this,
        tr("Success!"),
        tr("Room has been booked! Please ask for Govt. Id from customer") );
    }
}

//QString BookRoomDialog::getname() const{
//    return ui->txtName->text();

//}

//QString BookRoomDialog::getphone() const{
//    return ui->txtContactNumber->text();


//}

//int BookRoomDialog::combobox() const{
//    return ui->cmbRoomList->currentText().toInt();


//}
//QString BookRoomDialog::getaddres() const{
//    return ui->txtAddress->toPlainText();

//}
 
```
</details>

  
<details>
<summary>checkoutdialog.cpp</summary>
<br>
 
```
#include "checkoutdialog.h"
#include "ui_checkoutdialog.h"
#include "QDebug"

CheckOutDialog::CheckOutDialog(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::CheckOutDialog)
{
    ui->setupUi(this);
    this->setWindowTitle("Check out");
    this->setFixedSize(300,300);
    this->setWindowIcon(QIcon(":/check-out.jpg"));
    qDebug()<<"in constructor of CheckOutDialog";
}



void CheckOutDialog::readData()
{
    std::vector<int>rooms = Hotel::getInstance()->getRoomList("n");
    this->ui->comboBox->clear();

    char flag = 0;
    for(std::vector<int>::iterator it = rooms.begin(); it!=rooms.end(); it++ )
    {
        this->ui->comboBox->addItem(QString::number(*it));
        flag = 1;
    }

    if(flag==1) this->ui->btnCheckout->setEnabled(true);

}
CheckOutDialog::~CheckOutDialog()
{
    delete ui;
}

void CheckOutDialog::on_btnCancel_clicked()
{
    this->show();
}

void CheckOutDialog::on_btnCheckout_clicked()
{

    //call hotels's checkout
    int  roomno = ui->comboBox->currentText().toInt();

    if(roomno < 1)
    {
            QMessageBox::information(
            this,
            tr("Warning!"),
            tr("No room to Check out") );
            return;
     }
    int ret = Hotel::getInstance()->CheckOut(roomno);

    QString msg = "";
    ret==0?msg="Success!":"Failure!";

    this->hide();

    if(ret == 0)
    {
        QMessageBox::information(
        this,
        tr("Success!"),
        tr("Room has been Check-out! Say thank you to Customer") );
    }
}


//int CheckOutDialog::box() const{
//    return ui->comboBox->currentText().toInt();

//}
 
```
</details>
  
<details>
<summary>roomavailabledialog.cpp</summary>
<br>
 
```
#include "roomavailabledialog.h"
#include "ui_roomavailabledialog.h"
#include <QDebug>

RoomAvailableDialog::RoomAvailableDialog(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::RoomAvailableDialog)
{
    ui->setupUi(this);
    this->setFixedSize(380,200);
    this->setWindowTitle("Available room");
    qDebug()<<"In RoomAvailableDialog()";
    //this->setWindowIcon(QIcon(":/available.jpg"));


}

void RoomAvailableDialog::readData()
{
    qDebug()<<"in readData()";

    std::vector<int>rooms = Hotel::getInstance()->getRoomList("y");
    ui->lblinfo->setStyleSheet("QLabel { background-color : grey; color : aqua; }");

    std::vector<int>temprooms =  {101, 102, 103, 104, 105, 201, 202, 203, 204, 205};

    //set default color to all
    for(std::vector<int>::iterator it = temprooms.begin(); it!=temprooms.end(); it++ )
    {
        //Put logic to change color of Labels
        QString lblname = "lbl" + QString::number(*it);
        QLabel * ptr = this->findChild<QLabel*>(lblname);

        if(ptr)
        {
            ptr->setStyleSheet("QLabel { background-color : lightgrey; color : aqua; }");
        }

    }

    for(std::vector<int>::iterator it = rooms.begin(); it!=rooms.end(); it++ )
    {
        //Put logic to change color of Labels
        QString lblname = "lbl" + QString::number(*it);
        QLabel * ptr = this->findChild<QLabel*>(lblname);

        if(ptr)
        {
            //pLabel->setStyleSheet("QLabel { background-color : red; color : blue; }");

            ptr->setStyleSheet("QLabel { background-color : grey; color : aqua; }");
        }

    }
}

RoomAvailableDialog::~RoomAvailableDialog()
{
    qDebug()<<"Deleting RoomAvailableDialog";
    delete ui;
}

QString RoomAvailableDialog::groupBox()const{
        return ui->lbl101->text();
        return ui->lbl102->text();
        return ui->lbl103->text();
        return ui->lbl104->text();
        return ui->lbl105->text();
        return ui->lbl201->text();
        return ui->lbl202->text();
        return ui->lbl203->text();
        return ui->lbl204->text();
        return ui->lbl205->text();



}
void RoomAvailableDialog::on_pushButton_clicked()
{
    this->hide();
}
  
```
</details> 
  
<details>
<summary>transaction.cpp</summary>
<br>
 
```
#include "transaction.h"
#include "ui_transaction.h"

transaction::transaction(QWidget *parent) :
    QDialog(parent),
    ui(new Ui::transaction)
{
    ui->setupUi(this);
    this->setFixedSize(320,180);
    this->setWindowTitle("Transaction ");
   this->setWindowIcon(QIcon(":/transaction-icon.jpg"));

}
void transaction::readData()
{
    QSqlDatabase Database = QSqlDatabase::addDatabase("QSQLITE");
    Database.setDatabaseName("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data");
    if(QFile::exists("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data"))
        qDebug() << "DB file exist";
    else
       qDebug() << "DB file doesn't exists";

    if (!Database.open())
        qDebug() << Database.lastError().text();
    else
        qDebug() << "Database loaded successfull!";

    QSqlQuery query(Database);
    query.prepare("select * from cppbuzz_transaction");

    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    else
        qDebug() << "Update was successful "<< query.lastQuery();


     while(query.next())
     {

         this->ui->lstWidget->addItem(query.value(0).toString() +"************************"+ query.value(1).toString() +"****************"+ query.value(2).toString());
         qDebug() << query.value(0).toString() << " " << query.value(1).toString() << query.value(2).toString();
     }

     Database.close();
}
transaction::~transaction()
{
    delete ui;
}
  
```
</details>  
  
<details>
<summary>hotel.cpp</summary>
<br>
 
```
#include "hotel.h"
#include "QDebug"
#include<QMessageBox>
#include <checkoutdialog.h>

Hotel* Hotel::instance = nullptr;
int Hotel::CheckOut(int roomno)
{
    qDebug()<<"in CheckOut for room no : " << roomno;
    //**** update DB **********

    QSqlDatabase Database = QSqlDatabase::addDatabase("QSQLITE");
    Database.setDatabaseName("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data");
    if(QFile::exists("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data"))
        qDebug() << "DB file exist";
    else
       qDebug() << "DB file doesn't exists";

    if (!Database.open())
        qDebug() << Database.lastError().text();
    else
        qDebug() << "Database loaded successfull!";

    QSqlQuery query(Database);
    query.prepare("update cppbuzz_room set available ='y' where number='" +QString::number(roomno)+ "'");

    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    else
        qDebug() << "Update was successful "<< query.lastQuery();


    Database.close();
    //getRoomList();
    CheckOut(roomno);
    return 0;
}

int Hotel::BookRoom(int roomno, QString name, QString contactno, QString govtid, QString address)
{
    qDebug() << "in BookRoom for room no : "<< roomno;

    //**** update DB **********


    QSqlDatabase Database = QSqlDatabase::addDatabase("QSQLITE");
    Database.setDatabaseName("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data");
    if(QFile::exists("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data"))
        qDebug() << "DB file exist";
    else
       qDebug() << "DB file doesn't exists";

    if (!Database.open())
        qDebug() << Database.lastError().text();
    else
        qDebug() << "Database loaded successfull!";

   QSqlQuery query(Database);
 //query.prepare("insert into cppbuzz_room (number) values ('"+QString::number(roomno)+ "')");

    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    //prepare hotel room query
    query.prepare("update cppbuzz_room set available ='n' where number='" +QString::number(roomno)+ "'");
    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    else
        qDebug() << "Update was successful "<< query.lastQuery();

    //prepare customer query
    query.clear();
    query.prepare("insert into cppbuzz_customer (name, mobileno, govtid, address) values ('" + name + "','" + contactno + "','" + govtid + "','" + address + "')");
    QString customer_id;
    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    else
    {
        qDebug() << "Update was successful "<< query.lastQuery();
        customer_id = query.lastInsertId().toString();
        qDebug() <<"Last Inserted Id is  : "<< customer_id;
    }

    //prepare transaction query
    query.clear();
    query.prepare("insert into cppbuzz_transaction (room, customer_id) values ('" + QString::number(roomno) + "','" + customer_id + "')");
    if(!query.exec())
        qDebug() << query.lastError().text() << query.lastQuery();
    else
    {
        qDebug() <<"Update was successful "<< query.lastQuery();
        qDebug() <<"Last Inserted Id is  : "<<query.lastInsertId().toString();
    }




    Database.close();
    //getRoomList();
    return 0;
}

std::vector<int> Hotel::getRoomList(QString flag = "y")
{
        std::vector<int> rooms;
        //if(availableRooms.empty())
        QSqlDatabase Database = QSqlDatabase::addDatabase("QSQLITE");
        Database.setDatabaseName("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data");
        if(QFile::exists("C:\\Users\\Hsaine\\Desktop\\Hotel_Management_in_QT (1)\\Hotel_Management_in_QT (1)\\data"))
            qDebug() << "DB file exist";
        else
           qDebug() << "DB file doesn't exists";

        if (!Database.open())
            qDebug() << Database.lastError().text();
        else
            qDebug() << "Database loaded successfull!";

        QSqlQuery query(Database);
        query.prepare("select number from cppbuzz_room where available = '" + flag + "'");

        if(!query.exec())
            qDebug() << query.lastError().text() << query.lastQuery();
        else
            qDebug() << "Fetch was successful";

        while(query.next())
        {
            QString record = query.value(0).toString();
            rooms.push_back(record.toInt());
            qDebug()<<"Line is : "<<record;
        }

        Database.close();
        return rooms;
}

Hotel *Hotel::getInstance()
{
    if(instance == nullptr)
        instance = new Hotel();
    return instance;
}
  
```
</details>  
  
  
<details>
<summary>mainwindow.cpp</summary>
<br>
 
```
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include<QDebug>

MainWindow::MainWindow(QWidget *parent) :
    QMainWindow(parent),
    ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    this->setFixedSize(1000,1000);

    ptrRoomAvailableDlg = new RoomAvailableDialog(this);
    ptrCheckOutDlg = new CheckOutDialog(this);
    ptrRoomBookingDlg = new BookRoomDialog(this);
    ptrTransaction = new transaction(this);

    QPixmap pm(":/booking.jfif"); // <- path to image file
    ui->imgLabel->setPixmap(pm);
    ui->imgLabel->setScaledContents(true);
    this->setWindowTitle("Booking Hotel");   //title of the application
    this->setWindowIcon(QIcon(":/booking.jfif"));
}

MainWindow::~MainWindow()
{
    qDebug()<<"MainWindow: Deleting";
    delete ui;
    delete ptrRoomBookingDlg;
    delete ptrCheckOutDlg;
    delete ptrRoomAvailableDlg;
    delete ptrTransaction;
}

void MainWindow::on_btnRoomBooking_clicked()
{
    //create the dialog
//    BookRoomDialog D;
//    D.setModal(false);
//    //exécuter le dialogue
//    auto reply = D.exec();


//        if(reply == BookRoomDialog::Accepted)

    qDebug() <<this->metaObject()->className()<< ": In Room Booking";
    ptrRoomBookingDlg->readData();
    ptrRoomBookingDlg->show();

    if(ptrRoomBookingDlg->isVisible())
        qDebug()<<"New Window is visible";
    else
        qDebug()<<"New Window is not visible";
   // BookRoom();
}

void MainWindow::on_btnRoomCheckout_clicked()
{
    //create the dialog
//    CheckOutDialog D1;
//    D1.setModal(false);
//    auto reply1 = D1.exec();


//        if(reply1 == CheckOutDialog::Accepted)

    qDebug() <<this->metaObject()->className()<< ": In Room Checkout";
    ptrCheckOutDlg->readData();
    ptrCheckOutDlg->show();
}

void MainWindow::on_btnCheckAvailability_clicked()
{

    //create the dialog
//    RoomAvailableDialog D2;
//    D2.setModal(false);
//    auto reply2 = D2.exec();


//        if(reply2 == RoomAvailableDialog::Accepted)

    qDebug() <<this->metaObject()->className()<< ": In Check Availability";
    ptrRoomAvailableDlg->readData();
    ptrRoomAvailableDlg->show();
}

void MainWindow::on_bntTransaction_clicked()
{
    ptrTransaction->readData();
    ptrTransaction->show();
}

void MainWindow::on_actionAbout_Application_triggered()
{
    QMessageBox::about(this, "About Application","System Hotel Management is an appliaction "
"created by Qt Creator using C++,"
"is an application allow clients to"
" check the available of rooms "
"then you can book a room available,"
"after this operation we will show your"
" id_number that is mean your number as client in our service "
"when you click on Transaction Button,finnally when you want to "
"leave the hotel just check out for make the room available for other client.");
}


void MainWindow::on_actionAbout_QT_triggered()
{
    QMessageBox::aboutQt(this, "About QT");

}


void MainWindow::on_actionInformation_BARAHA_Hotel_triggered()
{
    QMessageBox::about(this, "About BARAHA HOTEL","Welcome to BARAHA HOTEL Is Hotel 3 Stars,the rooms from 101 to "
"105 are single rooms and the rooms from 201 to 205  are double.");

}


void MainWindow::on_actionExit_triggered()
{
    auto reply =QMessageBox::question(this,"Exit","Do you really want to quit our interface!");
    if(reply==QMessageBox::Yes){
        qApp->exit();
    }
}


void MainWindow::on_actionSingle_room_triggered()
{

    QMessageBox::about(this, "Single Room","2000$");
}


void MainWindow::on_actionDouble_room_triggered()
{
    QMessageBox::about(this, "Double Room","1500$");

}

 
    
```
</details>   
  
 
<details>
<summary>main.cpp</summary>
<br>
 
```
#include "mainwindow.h"
#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    MainWindow w;
    w.show();
    return a.exec();
}
 
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



















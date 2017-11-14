# testgit
图书信息库
create table book  (bnum nchar(20) primary key, 
bname nchar(20) not null,
 bauthor nchar(20) not null, 
bpublic nchar(20) not null, 
bclasses nchar(20) not null, 
benshu nchar(20) not null)；  
管理员登录库  
create table login  (loginnum nchar(20) primary key, 
name nchar(20) not null,  
loginpassword nchar(20) not null)；  
读者登录信息库  
create table reader  (usernum nchar(20) primary key, 
username nchar(20) not null, 
userytpe nchar(20) not null, 
userpassword nchar(20) not null)；  
读者信息库  
create table readerifo  (usernum nchar(20) primary key,
 username nchar(20) not null,
 usersex nchar(20) not null, 
usergrade nchar(20) not null,
 telephone nchar(20) not null)；
  借阅图书信息库 
 create table borrowifo (bnum nchar(20) primary key, 
bname nchar(20) not null, 
bauthor nchar(20) not null,
 bpublic nchar(20) not null,
 bclasses nchar(20) not null, 
benshu nchar(20) not null,
 btime date not null,
  usernum nchar(20) not null,
 username nchar(20) not null, 
usersex nchar(20) not null, 
登录模块  
if(username.Text.Trim()==""||password.Text.Trim()=="")    
 MessageBox.Show("请输入用户名和密码","提示");  
  else      
 {             
   if (radioManage.Checked == true)      
       {                 
  string strcon = "Data Source=SIMON-VAIO;Initial Catalog=lkl2;Integrated Security=True;";  //连接数据库的字符串，用于指定数据库地址，名称，账号，密码，连接方式               
   SqlConnection sqlCon = new SqlConnection(strcon);  //实例化并定义一个数据库连接             
    sqlCon.Open();  //打开数据库连接                
  string sql = "select * from login where usernum=@usernum and userpassword=@suerpassword";  //定义要查询sql语句   
  SqlCommand cmd = new SqlCommand(sql, sqlCon);    //实例化并定义sql语句和数据库路径   
  cmd.Parameters.Add("@usernum", SqlDbType.NChar, 20);  //定义cmd查询命令的字段属性，@loginname sqldbtype nchar（20）   
 cmd.Parameters.Add("@suerpassword", SqlDbType.NChar, 20);  //同上              
    cmd.Parameters["@usernum"].Value = username.Text;  //将username中的text保存到变量@loginname              
    cmd.Parameters["@suerpassword"].Value = password.Text;  //同上            
     SqlDataReader dr = cmd.ExecuteReader();                
 if (dr.Read())                               
  {
          this.Visible=false;                      
  Form2 Formmain = new Form2(); //应该是实例化一个主窗体的                     
this.Hide(); //应该是切换到主窗口的或关闭自己的                 
   Formmain.Show(); //应该是打开一个主窗体的                  
  dr.Close();//关闭dr的数据库连接                
   }                
  else  // if (dr.Read())读取失败则执行如下代码                                  
     MessageBox.Show("密码错误,请重新输入!");  //显示提示信息         
    }                        
else if (radioPerson.Checked==true)         
 {                
  string strcon = "Data Source=SIMON-VAIO;Initial Catalog=lkl2;Integrated Security=True;";  //连接数据库的字符串，用于指定数据库地址，名称，账号，密码，连接方式                 
 SqlConnection sqlCon = new SqlConnection(strcon);  //实例化并定义一个数据库连接                
 sqlCon.Open();  //打开数据库连接                 
 string sql1 = "select * from reader where usernum=@usernum and userpassword=@suerpassword";  //定义要查询sql语句       
 SqlCommand cmd1 = new SqlCommand(sql1, sqlCon);    //实例化并定义sql语句和数据库路径                 
cmd1.Parameters.Add("@usernum", SqlDbType.NChar, 20);  //定义cmd查询命令的字段属性，@loginname sqldbtype nchar（20）                 
 cmd1.Parameters.Add("@suerpassword", SqlDbType.NChar, 20);  //同上                  
cmd1.Parameters["@usernum"].Value = username.Text;  //将username中的text保存到变量@loginname                  
cmd1.Parameters["@suerpassword"].Value = password.Text;  //同上                
 cmd1.CommandText=sql1;                  
SqlDataReader dr = cmd1.ExecuteReader();         
 if (dr.Read())                  
{                      
this.Visible=false;                      
 Form9 Formmain = new Form9(); //应该是实例化一个主窗体的                     
this.Hide(); //应该是切换到主窗口的或关闭自己的                    
 dr.Close();//关闭dr的数据库连接                                
 Formmain.Show(); //应该是打开一个主窗体的                    
 }     
 else            
 MessageBox.Show("用户名或密码错ª误","警告");            
  }             
else                 
 MessageBox.Show("没有选择角色", "提示");

查询图书：
SqlConnection con = new SqlConnection();//建立数据库连接     
           
 con.ConnectionString = "Data Source=SIMON-VAIO;Initial Catalog=lkl2;Integrated Security=True;"; 
      
 con.Open();//打开连接 
            
SqlCommand cmd = new SqlCommand("select * from book where bname=@bname", con);             
cmd.Parameters.Add("@bname", SqlDbType.NChar, 20);            
 cmd.Parameters["@bname"].Value = bookname.Text;             
SqlDataAdapter da = new SqlDataAdapter(cmd);             
DataTable dt = new DataTable("图书记录表");            
 da.TableMappings.Add("BorrowRecord", "借阅记录表");             
da.TableMappings[0].ColumnMappings.Add("bnum", "图书号");            
 da.TableMappings[0].ColumnMappings.Add("bname", "图书名");            
 da.TableMappings[0].ColumnMappings.Add("bauthor", "作者");             
da.TableMappings[0].ColumnMappings.Add("bpublic", "出版社");             
da.TableMappings[0].ColumnMappings.Add("bclasses", "类别");             
da.TableMappings[0].ColumnMappings.Add("benshu", "本数");            
 da.Fill(dt); 
            
dataGridView1.DataSource = dt;             
con.Close();


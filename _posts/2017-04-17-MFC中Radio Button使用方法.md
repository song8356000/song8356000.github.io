---
title: MFC中Radio Button使用方法
date: 2019-04-02 17:18:57
tags: CSDN迁移
---
   先为对话框加上2个radio button，分别是Radio1和Radio2。

 问题1：如何让Radio1或者Radio2默认选上？如何知道哪个被选上了？

 关键是选上，“默认”只要放在OnInitDialog()即可。三种方法可以让它选上，  
 第一种：  
 ((CButton *)GetDlgItem(IDC_RADIO1))->SetCheck(TRUE);//选上  
 ((CButton *)GetDlgItem(IDC_RADIO1))->SetCheck(FALSE);//不选上  
 ((CButton *)GetDlgItem(IDC_RADIO1))->GetCheck();返回1表示选上，0表示没选上  
 第二种：  
 关联一个congtrol型变量（子类化），好ctrl+W(即打开classwizard),点开 Member Variables，咦？怎么没有IDC_RADIO1这个ID？原来是没有分组。因为radio button通常都是成组使用的，在一组里面是互斥的。取消，回到对话框资源面板，右键Radio1查看属性把Group选上，那么，Radio1和Radio2就是一组了（怎么知道他们是一组的？后面说）。此时，就可以为Radio1增加一congtrol型变量m_ctrlRadio1了。如下：  
 m_ctrlRadio1.SetCheck(TRUE);  
 同样可以使用GetCheck()获取状态。  
 第三种：  
 关联一个int型变量（同样需要先分组）m_nRadio1，打开对话框构造函数，你会发现有：  
 m_nRadio1 = -1;m_nRadio1别赋值-1表示哪个都没有选上。如果你把-1改成0，就会发现Radio1默认被选上了，依此类推，m_nRadio1的值为1就是第二个被选上了（这里同样有问题，哪个是第一个？哪个是第二个？）。获取状态很简单，UpdateData(TRUE)后判断m_nRadio1的值即可。

 问题2：如何使用多组？

 多组和一组是一样的使用，只要搞清楚哪个是哪一组的就行了。再为对话框添加Radio3和Radio4。很简单，先为这些Radio Button排个顺序，就是排列他们的TAB ORDER。在对话框资源面板上Ctrl+D，然后按你自己的理想顺序用鼠标逐个点击就可以了。不妨假设Radio1、Radio2、Radio3、Radio4分别是1、2、3、4。Radio1和Radio3都选上Group属性，那么，1、2是一组，3、4是另外一组，因为分组的原则是在选上Group属性的这一个开始直到碰到下一个选上Group属性的。你不妨再Ctrl+D，令Radio1、Radio2、Radio3、Radio4分别是1、3、2、4，那么Radio1和Radio3是一组，如果m_nRadio1=1,此时是Radio3被选上而不是Radio2被选上。分好了组就分别使用它们吧。

 嗯，也许你还要为它们添加鼠标单击事件，非常简单。

 一、对单选按钮进行分组：  
 每组的第一个单选按钮设置属性：Group，Tabstop，Auto;其余按钮设置属性Tabstop，Auto。如：  
 Radio1、Radio2、Radio3为一组，Radio4、Radio5为一组

 设定Radio1属性：Group，Tabstop，Auto  
 设定Radio2属性：Tabstop，Auto  
 设定Radio3属性：Tabstop，Auto

 设定Radio4属性：Group，Tabstop，Auto  
 设定Radio5属性：Tabstop，Auto

 二、用ClassWizard为单选控件定义变量，每组只能定义一个。如：m_Radio1、m_Radio4。

 三、用ClassWizard生成各单选按钮的单击消息函数，并加入内容：

 void CWEditView::OnRadio1()   
 {  
 m_Radio1 = 0; //第一个单选按钮被选中  
 }

 void CWEditView::OnRadio2()   
 {  
 m_Radio1 = 1; //第二个单选按钮被选中  
 }

 void CWEditView::OnRadio3()   
 {  
 m_Radio1 = 2; //第三个单选按钮被选中  
 }

 void CWEditView::OnRadio4()   
 {  
 m_Radio4 = 0; //第四个单选按钮被选中  
 }

 void CWEditView::OnRadio5()   
 {  
 m_Radio4 = 1; //第五个单选按钮被选中  
 }

 四、设置默认按钮：  
 在定义控件变量时，ClassWizard在构造函数中会把变量初值设为-1，只需把它改为其它值即可。  
 如：  
 //{{AFX_DATA_INIT(CUnitBlockTypeFlankPublicAdd)  
 m_Radio1 = 0; //初始时第一个单选按钮被选中  
 m_Radio4 = 0; //初始时第四个单选按钮被选中  
 //}}AFX_DATA_INIT  
 ---------------------   
  
 本文转载自：https://blog.csdn.net/abcjennifer/article/details/7476045   
 

   
 
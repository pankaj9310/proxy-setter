#!/usr/bin/python
#
#   "Super Proxy Setter"
#   with GTK Interface 
#
#   Ubuntu proxy setting tool.
#   This sets the apt,bash and profile config-files.
#   Network proxy-settings with user-name and password can only be configured with this tool .
#   
#   Supports Ubuntu 8.04 - Ubuntu 13.04 (Latest as of Sep 2013)

#   A tool to configure proxy-settings in universities and office environmment.
#   It Eliminates the need of doint editing again and again of system files that is prone to frequent manual errors.  
#   Atleast 3 different configuration files needs to be modified to configure proxy settings,
#   especially the network proxy-settings with username and password.
#   This can be used in an environment where ("http","https" and the "ftp") proxies have the same or different settings.
#   
#
#
#
#   Author:  Abdul Qadir Faridi , Pankaj Chaudhary
#
#   E-mail:  aqfaridi[@]gmail[.]com , pankaj9310[@]gmail[.]com
#
#   Date:    16/9/2013
#   Meta:   
#            Abdul Qadir Faridi , Pankaj Chaudhary
#            Linux Community 
#            ABV - Indian Institute of Information Technology and Management - Gwalior
#
#   Powered By:
#               Ubuntu 11.10 & Vi IMproved 7.3 
#   
#
#   Ver.- 1.0.0
#
#   ReadMe -  1) chmod 777 spsetter
#	      2) sudo ./spsetter	
#

import gtk
import pygtk
import os
import sys


class  Base :
    def destroy(self,widget,data=None):
        gtk.main_quit()
    def chkevent(self,widget):
        if widget.get_active():
            self.t2.set_text(self.t1.get_text())
            self.t3.set_text(self.t1.get_text())
            self.spinbutton1.set_value((self.spinbutton.get_value()))
            self.spinbutton2.set_value((self.spinbutton.get_value())) 

    def resett(self,widget):
        self.t1.set_text("")
        self.t2.set_text("")
        self.t3.set_text("")
        self.spinbutton.set_value(0)
        self.spinbutton1.set_value(0)
        self.spinbutton2.set_value(0)
        self.tuser.set_text("")
        self.tpwd.set_text("")
        self.chk.set_active(0)

    def sett(self,widget):
        f1 = open("/etc/apt/apt.conf","w+")
        f2 = open("/etc/environment","a")
        f3 = open("/etc/bash.bashrc","a")

        str1 = self.t1.get_text() 
        pstr1 = self.spinbutton.get_value()    
        str2 = self.t2.get_text()
        pstr2 = self.spinbutton1.get_value()
        str3 = self.t3.get_text()
        pstr3 = self.spinbutton2.get_value()
        uname = self.tuser.get_text()
        passwd = self.tpwd.get_text()
       
        if( len(str1)==0 or len(str2)==0 or len(str3)==0 or len(uname)==0 or len(passwd)==0 ): 
            em = gtk.MessageDialog ( None,0,gtk.MESSAGE_ERROR,gtk.BUTTONS_CLOSE,"Error ! Fill all Fields." )
            em.run()
            em.destroy()
            return     
   
        strhttp = "Acquire::http::proxy \"http://"+uname+":"+passwd+"@"+str1+":"+str(int(pstr1))+"/\";\n"
        strftp = "Acquire::ftp::proxy \"ftp://"+uname+":"+passwd+"@"+str2+":"+str(int(pstr2))+"/\";\n"
        strhttps = "Acquire::https::proxy \"https://"+uname+":"+passwd+"@"+str3+":"+str(int(pstr3))+"/\";"
        f1.write(strhttp)
        f1.write(strftp)
        f1.write(strhttps)
        f1.close()
        
        strhttpenv = "http_proxy=\"http://"+uname+":"+passwd+"@"+str1+":"+str(int(pstr1))+"\"\n"        
        strftpenv = "ftp_proxy=\"ftp://"+uname+":"+passwd+"@"+str2+":"+str(int(pstr2))+"\"\n"
        strhttpsenv = "https_proxy=\"https://"+uname+":"+passwd+"@"+str3+":"+str(int(pstr3))+"\""
        f2.write('\n')
        f2.write(strhttpenv)
        f2.write(strftpenv)
        f2.write(strhttpsenv)
        f2.close()
	f3.write('\n')	
        f3.write("export "+strhttpenv)
        f3.write("export "+strftpenv)
        f3.write("export "+strhttpsenv)
        f3.close()
    
        self.dialog = gtk.MessageDialog(None,0,gtk.MESSAGE_INFO,gtk.BUTTONS_OK,"Your Proxy has been set Properly.")
        self.dialog.format_secondary_text("Enjoy Download using terminal/software center.")
        response = self.dialog.run()
        if(response == gtk.RESPONSE_OK):
            gtk.main_quit()

        self.dialog.destroy()   
 
    def __init__(self):
        self.win = gtk.Window(gtk.WINDOW_TOPLEVEL)
        self.win.set_position(gtk.WIN_POS_CENTER)
        self.win.set_size_request(600,230)    
        self.win.set_title("Proxy-Setter")
        self.win.set_resizable(False)
        self.win.set_tooltip_text("This is proxy-setter - version 1.0")
        self.hbox = gtk.HBox()
        
        self.l1 = gtk.Label("HTTP Proxy :")
        self.t1 = gtk.Entry()
        self.l2 = gtk.Label("FTP Proxy : ")
        self.t2 = gtk.Entry()        
        self.l3 = gtk.Label("HTTPS Proxy :")
        self.t3 = gtk.Entry()

        self.p1 = gtk.Label("Port : ")
        self.p2 = gtk.Label("Port : ")
        self.p3 = gtk.Label("Port : ")
        
        self.tp1 = gtk.Entry()
        self.tp2 = gtk.Entry()
        self.tp3 = gtk.Entry()
        self.shift = gtk.Label(" ")
        self.chk = gtk.CheckButton()
        self.lchk = gtk.Label("Use this proxy server for all protocols")
        self.chk.connect("toggled",self.chkevent)    
    
        self.user = gtk.Label("Username : ")
        self.pwd = gtk.Label("Password : ")
        self.tuser = gtk.Entry()
        self.tpwd = gtk.Entry()
        self.tpwd.set_visibility(gtk.FALSE)
        self.vbox = gtk.VBox()
        self.hbox1 = gtk.HBox()
        self.hbox2 = gtk.HBox()


        self.b1 = gtk.Button("   Set   ")
        self.b1.connect("clicked",self.sett)
        self.b2 = gtk.Button("  Reset  ")
        self.b2.connect("clicked",self.resett) 
        self.hboxchk = gtk.HBox(spacing=0)
        self.hboxchk.pack_start(self.shift,False,False,63)
        self.hboxchk.pack_start(self.chk,False,False,0)
        self.hboxchk.pack_start(self.lchk,False,False,0)
        
        self.hbox.pack_start(self.l1,False,False,24)
        self.adjustment = gtk.Adjustment(3128, 0, 15000, 1, 10, 0)        
        self.adjustment1 = gtk.Adjustment(3128, 0, 15000, 1, 10, 0)
        self.adjustment2 = gtk.Adjustment(3128, 0, 15000, 1, 10, 0)
        
        self.spinbutton = gtk.SpinButton()
        self.spinbutton1 = gtk.SpinButton()
        self.spinbutton2 = gtk.SpinButton()
        self.spinbutton.set_adjustment(self.adjustment)
        self.spinbutton1.set_adjustment(self.adjustment1)
        self.spinbutton2.set_adjustment(self.adjustment2)
   
        self.hbox1.pack_start(self.l2,False,False,27)
        self.hbox2.pack_start(self.l3,False,False,20)

        self.hbox.pack_start(self.t1)
        self.hbox1.pack_start(self.t2)
        self.hbox2.pack_start(self.t3)

        self.hbox.pack_start(self.p1)
        self.hbox1.pack_start(self.p2)
        self.hbox2.pack_start(self.p3)

        #self.hbox.pack_start(self.tp1)
        self.hbox.pack_start(self.spinbutton, False, False, 0)        
        self.hbox1.pack_start(self.spinbutton1, False, False, 0)
        self.hbox2.pack_start(self.spinbutton2, False, False, 0)

        self.vbox.pack_start(self.hbox)
        self.vbox.pack_start(self.hboxchk)       
        self.vbox.pack_start(self.hbox1)
        self.vbox.pack_start(self.hbox2)

        self.hbox3 = gtk.HBox()
        self.hbox4 = gtk.HBox()      
        self.hbox5 = gtk.HBox()

        self.hbox3.pack_start(self.user)
        self.hbox4.pack_start(self.pwd)
        self.hbox5.pack_start(self.b1)
        self.hbox3.pack_start(self.tuser)
        self.hbox4.pack_start(self.tpwd)
        self.hbox5.pack_start(self.b2)

        self.vbox.pack_start(self.hbox3)
        self.vbox.pack_start(self.hbox4)
        self.vbox.pack_start(self.hbox5)

        self.win.add(self.vbox)
        self.win.show_all()
        self.win.connect("destroy",self.destroy)    
        
        
    def main(self):
        gtk.main()

if __name__ == "__main__" :
    base = Base()
    base.main()      
      
    

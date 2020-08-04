def mail_send(toaddr, filename):

              faddr = 'Your Email address'
              taddr = toaddr
              
              
              msg = MIMEMultipart()
              
              msg['From']=faddr
              msg['To']=taddr
              msg['Subject']="Attachment"
              
              body = "Hello Please find the attachment" 
              
              msg.attach(MIMEText(body, 'plain'))
              
              
              # /Users/Arpitsingh/Desktop/ Replace this with your files address
              attachment = open("/%s"%filename,"rb")
              
              part = MIMEBase('application', 'octet-stream')
              part.set_payload((attachment).read())
              encoders.encode_base64(part)
              part.add_header('Content-Disposition', "attachment; file_name= %s"%attachment)
              
              msg.attach(part)
              
              server = smtplib.SMTP('smtp.gmail.com','587')
              server.starttls()
              server.login(faddr, 'Your password')
              text = msg.as_string()
              server.sendmail(faddr,taddr,text)
              server.quit()
              print("Mail sent")

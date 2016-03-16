---
layout: post
title: Mockito - ArgumentCaptor to see email content
---

Mockito provides a nice way to capture the arguments passed into your
mocks. This works a treat when verifying the contents of an email send
via a mocked JavaMailSender








    ArgumentCaptor messageCapture = ArgumentCaptor.forClass(Multipart.class);
            Mockito.verify(mockMimeMessage).setContent(messageCapture.capture());
            
            //this is a multipart message so read all parts and verify
            StringWriter writer = new StringWriter();
            IOUtils.copy(messageCapture.getValue().getBodyPart(0).getInputStream(), writer, "UTF-8");
            String emailMessage = writer.toString();
            
            //verify the email doesn't contain the voucher content
            Assert.assertFalse(StringUtils.contains(emailMessage, "test content"));



 










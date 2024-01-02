var
//Kol
  FormKol  : TclGameForm;
  PanelFrmBottom : TclProPanel;
  LayoutMoveLeft , LayoutMoveRight  : TClLayout;
  BtnLeft , BtnRight , BtnUp , BtnDown : TclProButton;
  LblDurum , LblPlayerID : TClProLabel;
  ImgPlayer , ImgBckBtn : TClProImage
  TimerReso : TCLTimer;
  MYDeviceManager : TclDeviceManager;
  PlayerGuid , Player1 , Player2 : String;
  MqttKol : TclMQTT;
  Oyuncu : TclStringList;
  
  //Ekran
  FormEkran : TclGameForm;
  ButtonRestart , ButtonStartGame : TClProButton;
  ImagePlayer1 , ImagePlayer2 , ImageAst1 , ImageAst2 , ImageAst3 , ImageAst4 , ImageAst5 , ImageAst6 , ImageBtnBack , ImageStar1 , ImageStar2 , ImageStar3 , ImageStar4 , ImageStar5: TClProImage;
  TimerGame , TimerScore , TimerResolutionGame  : TCLTimer;
  LabelDurum , LabelPassword , LabelScore , LabelPlayer1 , LabelPlayer2: TClProLabel;
  score , Distance1 , Distance2 , Distance3 , Distance4 , Distance5 , Distance6 , Distance8 , Distance9 , Distance10 , Distance11 , Distance12 : Integer;
  MqttEkran : TclMQTT;
  
//kOL
  procedure ResolutionCtrl;
  begin
    if(TForm(FormKol).ClientWidth < TForm(FormKol).ClientHeight)then
    begin
     PanelFrmBottom.Width := TForm(FormKol).ClientWidth;
     PanelFrmBottom.Height := TForm(FormKol).ClientHeight / 2.5;

     LayoutMoveRight.Width := PanelFrmBottom.Width / 3;
     LayoutMoveRight.Height := PanelFrmBottom.Height;
    
     LayoutMoveLeft.Width := PanelFrmBottom.Width / 3;
     LayoutMoveLeft.Height := PanelFrmBottom.Height;
    
     BtnUp.Width := LayoutMoveRight.Width / 5;
     BtnUp.Height := LayoutMoveRight.Height / 2;
      
     BtnDown.Width := LayoutMoveLeft.Width / 5;
     BtnDown.Height := LayoutMoveLeft.Height / 2;
      
     BtnLeft.Width := LayoutMoveLeft.Width / 5;
     BtnLeft.Height := LayoutMoveLeft.Height / 2;
      
     BtnRight.Width := LayoutMoveRight.Width / 5;
     BtnRight.Height := LayoutMoveRight.Height / 2;
     
     ImgPlayer.Width := TForm(FormKol).ClientWidth/ 4;
     ImgPlayer.Height := TForm(FormKol).ClientHeight / 8;

     ImgBckBtn.Width := TForm(FormKol).ClientWidth / 8;
     ImgBckBtn.Height := TForm(FormKol).ClientHeight / 8;
     ImgBckBtn.Position.X := TForm(FormKol).ClientWidth / 50;
     ImgBckBtn.Position.Y := 0;

     LblDurum.Position.X := TForm(FormKol).ClientWidth - 105;
     LblDurum.Position.Y := 5;
    end;
    else if(TForm(FormKol).ClientWidth > TForm(FormKol).ClientHeight)then
    begin
     PanelFrmBottom.Width := TForm(FormKol).ClientWidth;
     PanelFrmBottom.Height := TForm(FormKol).ClientHeight / 2.5;
    
     LayoutMoveRight.Width := PanelFrmBottom.Width / 3;
     LayoutMoveRight.Height := PanelFrmBottom.Height;
    
     LayoutMoveLeft.Width := PanelFrmBottom.Width / 3;
     LayoutMoveLeft.Height := PanelFrmBottom.Height;
  
     BtnUp.Width := LayoutMoveRight.Width / 7;
     BtnUp.Height := LayoutMoveRight.Height / 2;
    
     BtnDown.Width := LayoutMoveLeft.Width / 7;
     BtnDown.Height := LayoutMoveLeft.Height / 2;
    
     BtnLeft.Width := LayoutMoveLeft.Width / 7;
     BtnLeft.Height := LayoutMoveLeft.Height / 2;
    
     BtnRight.Width := LayoutMoveRight.Width / 7;
     BtnRight.Height := LayoutMoveRight.Height / 2;
    
     ImgPlayer.Width := TForm(FormKol).ClientWidth/ 3;
     ImgPlayer.Height := TForm(FormKol).ClientHeight / 6;
    
     ImgBckBtn.Width := TForm(FormKol).ClientWidth / 7;
     ImgBckBtn.Height := TForm(FormKol).ClientHeight / 7;
     ImgBckBtn.Position.X := (TForm(FormKol).ClientWidth / 2) - (TForm(FormKol).ClientWidth / 1.975);
     ImgBckBtn.Position.Y := 5;

     LblDurum.Position.X := TForm(FormKol).ClientWidth - 105;
     LblDurum.Position.Y := 5;
      end;
  end;
  procedure MqttStatusChanged;
  begin
    if (MqttKol.Connected) then
    begin
      LblDurum.Text := 'Connected';
      clComponent.SetupComponent(LblDurum , '{"TextColor":"#279EFF"}');
      MqttKol.Send(Clomosy.AppUserGUID + ':RIGHT');
    end;
    else
    begin
      LblDurum.Text := 'Not Connected';
      clComponent.SetupComponent(LblDurum , '{"TextColor":"#952323"}');
      MqttKol.Connect;
    end;
  end;
  Procedure PublisMqttKol;
  begin
    Oyuncu := Clomosy.StringListNew;
    Oyuncu.Delimiter := ':';
    Oyuncu.DelimitedText := MqttKol.ReceivedMessage; 

    if(MqttKol.ReceivedMessage = 'Die')then
    begin
      MYDeviceManager.Vibrate(1000);
    end;
    if(Clomosy.StringListItemString(Oyuncu,1) = 'Oyuncu1')and(Clomosy.AppUserGUID = Clomosy.StringListItemString(Oyuncu,0))then
    begin
      LblPlayerID.Visible := True;
      LblPlayerID.Caption := 'OYUNCU 1';
    end;
    if(Clomosy.StringListItemString(Oyuncu,1) = 'Oyuncu2')and(Clomosy.AppUserGUID = Clomosy.StringListItemString(Oyuncu,0))then
    begin
      LblPlayerID.Visible := True;
      LblPlayerID.Caption := 'OYUNCU 2';
    end;
  end;
  Procedure Right;
  begin
   MqttKol.Send(Clomosy.AppUserGUID+':RIGHT');
  end;
  Procedure Left;
  begin
   MqttKol.Send(Clomosy.AppUserGUID + ':LEFT');
  end;
  Procedure Up;
  begin
   MqttKol.Send(Clomosy.AppUserGUID+':UP');
  end;
  Procedure Down;
  begin
   MqttKol.Send(Clomosy.AppUserGUID + ':DOWN');
  end;
  procedure CloseForm;
  begin
    TclProButton(FormKol.clFindComponent('BtnGoBack')).Click;
  end;
  

  
  procedure CreateKol;
  begin
    FormKol := TclGameForm.Create(Self);
    FormKol.SetFormBGImage('https://i.hizliresim.com/ngg8s2l.jpg');
    
    LblDurum := FormKol.AddNewProLabel(FormKol , 'LblDurum' , 'CONNECT');
    LblDurum.Align := alNone;
    clComponent.SetupComponent(LblDurum , '{"TextColor":"#952323" , "TextSize":15 , "TexteBold":"yes" , "TextHorizontalAlign":"center" , "TextVerticalAlign":"center"}');
    
    LblPlayerID := FormKol.AddNewProLabel(FormKol , 'LblPlayerID' , '');
    LblPlayerID.Align := alTop;
    LblPlayerID.Visible := False;
    LblPlayerID.Width := TForm(FormKol).ClientWidth;
    LblPlayerID.Height := TForm(FormKol).ClientHeight / 8;
    clComponent.SetupComponent(LblPlayerID , '{"TextColor":"#ffffff" , "TextSize":15 , "TexteBold":"yes" , "TextHorizontalAlign":"center" , "TextVerticalAlign":"center"}');
    
    MqttKol := FormKol.AddNewMQTTConnection(FormKol , 'MqttKol');
    FormKol.AddNewEvent(MqttKol , tbeOnMQTTStatusChanged , 'MqttStatusChanged');
    FormKol.AddNewEvent(MqttKol , tbeOnMQTTPublishReceived , 'PublisMqttKol');
    MqttKol.Channel := EditPasword.Text;
    MqttKol.Connect;
    
    PanelFrmBottom := FormKol.AddNewProPanel(FormKol , 'PanelFrmBottom');
    PanelFrmBottom.Align := alBottom;
     //clComponent.SetupComponent(PanelFrmBottom , '{"BackGroundColor":"#000000"}');
    
    LayoutMoveLeft := FormKol.AddNewLayout(PanelFrmBottom , 'LayoutMoveLeft');
    LayoutMoveLeft.Align := alLeft;
    LayoutMoveLeft.Width := PanelFrmBottom.Width / 2;
    
    LayoutMoveRight:= FormKol.AddNewLayout(PanelFrmBottom , 'LayoutMoveRight');
    LayoutMoveRight.Align := alRight;
    LayoutMoveRight.Width := PanelFrmBottom.Width / 2;
    
    BtnUp := FormKol.AddNewProButton(LayoutMoveRight , 'BtnUp' , 'İLERİ');
    BtnUp.Align := alTop;
    clComponent.SetupComponent(BtnUp , '{"BackGroundColor":"null" , "RoundWidth":10 , "RoundHeight":10 , "BorderColor":"#ffffff" , "BorderWidth":3 , "TextColor":"#ffffff" , "TexteBold":"yes" , "TextSize":25}');
    FormKol.AddNewEvent(BtnUp , tbeOnClick , 'Up');
    
    BtnDown := FormKol.AddNewProButton(LayoutMoveLeft , 'BtnDown' , 'GERİ');
    BtnDown.Align := alTop;
    clComponent.SetupComponent(BtnDown , '{"BackGroundColor":"null" , "RoundWidth":10 , "RoundHeight":10 , "BorderColor":"#ffffff" , "BorderWidth":3 , "TextColor":"#ffffff" , "TexteBold":"yes" , "TextSize":25}');
    FormKol.AddNewEvent(BtnDown , tbeOnClick , 'Down');
    
    BtnLeft := FormKol.AddNewProButton(LayoutMoveLeft , 'BtnLeft' , 'SOL');
    BtnLeft.Align := alBottom;
    clComponent.SetupComponent(BtnLeft , '{"BackGroundColor":"null" , "RoundWidth":10 , "RoundHeight":10 , "BorderColor":"#ffffff" , "BorderWidth":3 , "TextColor":"#ffffff" , "TexteBold":"yes" , "TextSize":25}');
    FormKol.AddNewEvent(BtnLeft , tbeOnClick , 'Left');
    
    BtnRight := FormKol.AddNewProButton(LayoutMoveRight , 'BtnRight' , 'SAĞ');
    BtnRight.Align := alBottom;
    clComponent.SetupComponent(BtnRight , '{"BackGroundColor":"null" , "RoundWidth":10 , "RoundHeight":10 , "BorderColor":"#ffffff" , "BorderWidth":3 , "TextColor":"#ffffff" , "TexteBold":"yes" , "TextSize":25}');
    FormKol.AddNewEvent(BtnRight , tbeOnClick , 'Right');
    
    ImgBckBtn := FormKol.AddNewProImage(FormKol , 'ImgBckBtn');
    ImgBckBtn.Align := alNone;
    clComponent.SetupComponent(ImgBckBtn , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/7945/7945195.png"}'); 
    FormKol.AddNewEvent(ImgBckBtn , tbeOnClick , 'CloseForm');
    
    ImgPlayer := FormKol.AddNewProImage(FormKol , 'ImgPlayer');
    ImgPlayer.Align := alCenter;
    ImgPlayer.Margins.Top := 50;



      
  
     //CREATE TIMER
    TimerReso := FormKol.AddNewTimer(FormKol , 'TimerReso' , 1);
    TimerReso.Enabled := True;
    FormKol.AddNewEvent(TimerReso , tbeOnTimer , 'ResolutionCtrl');

    MYDeviceManager := TclDeviceManager.Create;
  
    FormKol.Run;
  end;
  
  
  
  
  procedure Start;
  begin
    TimerScore.Enabled := True;
    LabelPassword.Visible := False;
    TimerGame.Enabled := True;
    ButtonRestart.Visible := False;
    LabelScore.Visible := True;
    ButtonStartGame.Visible := False;
  end;
  
  procedure CrashMeteor;
  begin
   if(clomosy.GlobalVariableInteger = 1)then
   begin
     Distance1 := Sqrt(Sqr(ImageAst1.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst1.Position.Y - ImagePlayer1.Position.Y));
     Distance2 := Sqrt(Sqr(ImageAst2.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst2.Position.Y - ImagePlayer1.Position.Y));
     Distance3 := Sqrt(Sqr(ImageAst3.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst3.Position.Y - ImagePlayer1.Position.Y));
     Distance4 := Sqrt(Sqr(ImageAst4.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst4.Position.Y - ImagePlayer1.Position.Y));
     Distance5 := Sqrt(Sqr(ImageAst5.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst5.Position.Y - ImagePlayer1.Position.Y));
     Distance6 := Sqrt(Sqr(ImageAst6.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst6.Position.Y - ImagePlayer1.Position.Y));
   end;
   else
   begin
     Distance1 := Sqrt(Sqr(ImageAst1.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst1.Position.Y - ImagePlayer1.Position.Y));
     Distance2 := Sqrt(Sqr(ImageAst2.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst2.Position.Y - ImagePlayer1.Position.Y));
     Distance3 := Sqrt(Sqr(ImageAst3.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst3.Position.Y - ImagePlayer1.Position.Y));
     Distance4 := Sqrt(Sqr(ImageAst4.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst4.Position.Y - ImagePlayer1.Position.Y));
     Distance5 := Sqrt(Sqr(ImageAst5.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst5.Position.Y - ImagePlayer1.Position.Y));
     Distance6 := Sqrt(Sqr(ImageAst6.Position.X - ImagePlayer1.Position.X) + Sqr(ImageAst6.Position.Y - ImagePlayer1.Position.Y));
     Distance8 := Sqrt(Sqr(ImageAst2.Position.X - ImagePlayer2.Position.X) + Sqr(ImageAst2.Position.Y - ImagePlayer2.Position.Y));
     Distance9 := Sqrt(Sqr(ImageAst3.Position.X - ImagePlayer2.Position.X) + Sqr(ImageAst3.Position.Y - ImagePlayer2.Position.Y));
     Distance10 := Sqrt(Sqr(ImageAst4.Position.X - ImagePlayer2.Position.X) + Sqr(ImageAst4.Position.Y - ImagePlayer2.Position.Y));
     Distance11 := Sqrt(Sqr(ImageAst5.Position.X - ImagePlayer2.Position.X) + Sqr(ImageAst5.Position.Y - ImagePlayer2.Position.Y));
     Distance12 := Sqrt(Sqr(ImageAst6.Position.X - ImagePlayer2.Position.X) + Sqr(ImageAst6.Position.Y - ImagePlayer2.Position.Y));
   end;
  end;
    
  procedure IncementScore;
  begin
   if(clomosy.GlobalVariableInteger = 1)then
   begin
    LabelScore.Text := IntToStr(score);
   end;
   score := score + 5;
  end;
//Ekran
  procedure CtrlResolotuion; //Çözünürlük Kontrolü.
  begin
    if(TForm(FormEkran).ClientWidth < TForm(FormEkran).ClientHeight)then //Ekran Dikeyse...
    begin
     if(TimerGame.Enabled = True)then
     begin
       ImageAst1.Visible := True;
       ImageAst2.Visible := True;
       ImageAst3.Visible := True;
       ImageAst4.Visible := True;
       ImageAst5.Visible := True;
       ImageAst6.Visible := False;
       ImageAst1.Width := TForm(FormEkran).ClientWidth / 4;
       ImageAst1.Height := TForm(FormEkran).ClientHeight / 12;
       ImageAst2.Width := TForm(FormEkran).ClientWidth / 4;
       ImageAst2.Height := TForm(FormEkran).ClientHeight / 12;
       ImageAst3.Width := TForm(FormEkran).ClientWidth / 6;
       ImageAst3.Height := TForm(FormEkran).ClientHeight / 14;
       ImageAst4.Width := TForm(FormEkran).ClientWidth / 8;
       ImageAst4.Height := TForm(FormEkran).ClientHeight / 10;
       ImageAst5.Width := TForm(FormEkran).ClientWidth / 5;
       ImageAst5.Height := TForm(FormEkran).ClientHeight / 14;
       ImageAst6.Width := TForm(FormEkran).ClientWidth / 4;
       ImageAst6.Height := TForm(FormEkran).ClientHeight / 12;
     end;
    else
    begin
     if(clomosy.GlobalVariableInteger = 1)then
     begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 75;
       ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 10;
     end;
     else
     begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 75;
       ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer2.Position.X := (TForm(FormEkran).ClientWidth / 2);
       ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 10;
       ImagePlayer2.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer2.Height := TForm(FormEkran).ClientHeight / 10;
     end;

    end;
     ImageBtnBack.Width := TForm(FormEkran).ClientWidth / 7;
     ImageBtnBack.Height := TForm(FormEkran).ClientHeight / 7;
     ImageBtnBack.Position.X := TForm(FormEkran).ClientWidth / 16;
     ImageBtnBack.Position.Y := 0;
     LabelDurum.Position.X := TForm(FormEkran).ClientWidth - 100;
     LabelDurum.Position.Y := 5;
     ButtonStartGame.Width := TForm(FormEkran).ClientWidth / 2;
     ButtonStartGame.Height := TForm(FormEkran).ClientHeight / 8;

if(clomosy.GlobalVariableInteger = 1)then
begin
    if ImagePlayer1.Position.X < 0 then
    begin
      ImagePlayer1.Position.X := 0;
    end;
    if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
    begin
      ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
    end;
    if ImagePlayer1.Position.Y < 0 then
    begin
       ImagePlayer1.Position.Y := 0;
    end;
    if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
    begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
    end;
end;
else
begin
    if ImagePlayer1.Position.X < 0 then
    begin
      ImagePlayer1.Position.X := 0;
    end;
    if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
    begin
      ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
    end;
    if ImagePlayer1.Position.Y < 0 then
    begin
       ImagePlayer1.Position.Y := 0;
    end;
    if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
    begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
    end;
    
    if ImagePlayer2.Position.X < 0 then
    begin
      ImagePlayer2.Position.X := 0;
    end;
    if (ImagePlayer2.Position.X + ImagePlayer2.Width) > TForm(FormEkran).ClientWidth then
    begin
      ImagePlayer2.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer2.Width;
    end;
    if ImagePlayer2.Position.Y < 0 then
    begin
       ImagePlayer2.Position.Y := 0;
    end;
    if ImagePlayer2.Position.Y  > TForm(FormEkran).ClientHeight then
    begin
       ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 100;
    end;

end;

    end;
    else if(TForm(FormEkran).ClientWidth > TForm(FormEkran).ClientHeight)then
    begin
     if(TimerGame.Enabled = True)then
     begin
     ImageAst1.Visible := True;
     ImageAst2.Visible := True;
     ImageAst3.Visible := True;
     ImageAst4.Visible := True;
     ImageAst5.Visible := True;
     ImageAst6.Visible := True;
     ImageAst1.Width := TForm(FormEkran).ClientWidth / 4;
     ImageAst1.Height := TForm(FormEkran).ClientHeight / 12;
     ImageAst2.Width := TForm(FormEkran).ClientWidth / 6;
     ImageAst2.Height := TForm(FormEkran).ClientHeight / 12;
     ImageAst3.Width := TForm(FormEkran).ClientWidth / 6;
     ImageAst3.Height := TForm(FormEkran).ClientHeight / 12;
     ImageAst4.Width := TForm(FormEkran).ClientWidth / 6;
     ImageAst4.Height := TForm(FormEkran).ClientHeight / 12;
     ImageAst5.Width := TForm(FormEkran).ClientWidth / 8;
     ImageAst5.Height := TForm(FormEkran).ClientHeight / 12;
     ImageAst6.Width := TForm(FormEkran).ClientWidth / 6;
     ImageAst6.Height := TForm(FormEkran).ClientHeight / 12;
     end;
    else
    begin
     if(clomosy.GlobalVariableInteger = 1)then
     begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 25;
       ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 10;
     end;
     else
     begin
       ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 25;
       ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 75;
       ImagePlayer2.Position.X := (TForm(FormEkran).ClientWidth / 2) - 100;
       ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 10;
       ImagePlayer2.Width := TForm(FormEkran).ClientWidth / 5;
       ImagePlayer2.Height := TForm(FormEkran).ClientHeight / 10;
     end;
    end;
    end;
    ImageBtnBack.Width := TForm(FormEkran).ClientWidth / 7;
    ImageBtnBack.Height := TForm(FormEkran).ClientHeight / 7;
    ImageBtnBack.Position.X := 0;
    ImageBtnBack.Position.Y := 5;

    
    LabelDurum.Position.X := TForm(FormEkran).ClientWidth - 100;
    LabelDurum.Position.Y := 5;
     
    ButtonStartGame.Width := TForm(FormEkran).ClientWidth / 4;
    ButtonStartGame.Height := TForm(FormEkran).ClientHeight / 8;
    
    if(clomosy.GlobalVariableInteger = 2)then
    begin
      if ImagePlayer1.Position.X < 0 then
      begin
        ImagePlayer1.Position.X := 0;
      end;
      if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
      end;
      if ImagePlayer1.Position.Y < 0 then
      begin
         ImagePlayer1.Position.Y := 0;
      end;
      if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
      
      if ImagePlayer2.Position.X < 0 then
      begin
        ImagePlayer2.Position.X := 0;
      end;
      if (ImagePlayer2.Position.X + ImagePlayer2.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer2.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer2.Width;
      end;
      if ImagePlayer2.Position.Y < 0 then
      begin
         ImagePlayer2.Position.Y := 0;
      end;
      if ImagePlayer2.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
    end;
    else
    begin
      if ImagePlayer1.Position.X < 0 then
      begin
        ImagePlayer1.Position.X := 0;
      end;
      if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
      end;
      if ImagePlayer1.Position.Y < 0 then
      begin
         ImagePlayer1.Position.Y := 0;
      end;
      if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
    end;
  end;
  procedure StatusChanged;
  begin
    if (MqttEkran.Connected) then
    begin
      LabelDurum.Text := 'Connected';
      clComponent.SetupComponent(LabelDurum , '{"TextColor":"#279EFF"}');
    end;
    else
    begin
      LabelDurum.Text := 'Not Connected';
      clComponent.SetupComponent(LabelDurum , '{"TextColor":"#952323"}');
      MqttEkran.Connect;
    end;
  end;
  
  procedure Movement;
  begin
   if(clomosy.GlobalVariableInteger = 1)then
   begin
    LabelPlayer1.Visible := True;
   end;
   else
   begin
    LabelPlayer1.Visible := True;
    LabelPlayer2.Visible := True;
   end;

    if(POS('RIGHT' , MqttEkran.ReceivedMessage) > 0)then
    begin
      if PlayerGuid = Player1 then
      begin
        ImagePlayer1.Position.X := ImagePlayer1.Position.X + 55;
        if(not clomosy.AppUserDisplayName)then
        begin
        end;
      end;
      if PlayerGuid = Player2 then
      begin
        ImagePlayer2.Position.X := ImagePlayer2.Position.X + 55;
      end;
    end;
    if(POS('LEFT' , MqttEkran.ReceivedMessage) > 0)then
    begin
      if PlayerGuid = Player1 then
      begin
        ImagePlayer1.Position.X := ImagePlayer1.Position.X - 55;
      end;
      if PlayerGuid = Player2 then
      begin
        ImagePlayer2.Position.X := ImagePlayer2.Position.X - 55;
      end;
    end;
    if(POS('UP' , MqttEkran.ReceivedMessage) > 0)then
    begin
      if PlayerGuid = Player1 then
      begin
        ImagePlayer1.Position.Y := ImagePlayer1.Position.Y - 55;
      end;
      if PlayerGuid = Player2 then
      begin
        ImagePlayer2.Position.Y := ImagePlayer2.Position.Y - 55;
      end;
    end;
    if(POS('DOWN' , MqttEkran.ReceivedMessage) > 0)then
    begin
      if PlayerGuid = Player1 then
      begin
        ImagePlayer1.Position.Y := ImagePlayer1.Position.Y + 55;
      end;
      if PlayerGuid = Player2 then
      begin
        ImagePlayer2.Position.Y := ImagePlayer2.Position.Y + 55;
      end;
    end;
    
    
    if(clomosy.GlobalVariableInteger = 2)then
    begin
      if ImagePlayer1.Position.X < 0 then
      begin
        ImagePlayer1.Position.X := 0;
      end;
      if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
      end;
      if ImagePlayer1.Position.Y < 0 then
      begin
         ImagePlayer1.Position.Y := 0;
      end;
      if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
      
      if ImagePlayer2.Position.X < 0 then
      begin
        ImagePlayer2.Position.X := 0;
      end;
      if (ImagePlayer2.Position.X + ImagePlayer2.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer2.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer2.Width;
      end;
      if ImagePlayer2.Position.Y < 0 then
      begin
         ImagePlayer2.Position.Y := 0;
      end;
      if ImagePlayer2.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
    end;
    else
    begin
      if ImagePlayer1.Position.X < 0 then
      begin
        ImagePlayer1.Position.X := 0;
      end;
      if (ImagePlayer1.Position.X + ImagePlayer1.Width) > TForm(FormEkran).ClientWidth then
      begin
        ImagePlayer1.Position.X := TForm(FormEkran).ClientWidth - ImagePlayer1.Width;
      end;
      if ImagePlayer1.Position.Y < 0 then
      begin
         ImagePlayer1.Position.Y := 0;
      end;
      if ImagePlayer1.Position.Y  > TForm(FormEkran).ClientHeight then
      begin
         ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 100;
      end;
    end;
    CrashMeteor;
  end;
  
  procedure PublisStatut;
  begin
   if(MqttEkran.ReceivedAlRight)then
   begin
     if (Trim(MqttEkran.ReceivedMessage) <> '') then
     begin
       PlayerGuid := Trim(CLGetStringTo(MqttEkran.ReceivedMessage , ':'));
       if Player1 = '' then
       begin
         Player1 := PlayerGuid;
         LabelPlayer1.Text := 'Oyuncu1';
       end;
       else if (Player2 = '') and (Player1 <> PlayerGuid) then
       begin
         Player2 := PlayerGuid;
         LabelPlayer2.Text := 'Oyuncu2';
       end;
     end;
    end;
   Movement;
  end;
  
  procedure CreateAsteroid //Asteroidlerin oluşturulmasını sağlayan prosedür.
  begin
   ImageAst1 := FormEkran.AddNewProImage(FormEkran , 'ImageAst1');
   ImageAst1.Align := alNone;
   ImageAst1.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst1.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst1 , '{"ImgUrl":"https://i.hizliresim.com/13gydwz.png"}');
   ImageAst1.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst1.Position.Y := -200;
   ImageAst1.Visible := False;
   clRTMethod(ImageAst1 , 'SendToBack');

   ImageAst2 := FormEkran.AddNewProImage(FormEkran , 'ImageAst2');
   ImageAst2.Align := alNone;
   ImageAst2.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst2.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst2 , '{"ImgUrl":"https://i.hizliresim.com/ehmehur.png"}');
   ImageAst2.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst2.Position.Y := -200;
   ImageAst2.Visible := False;
   clRTMethod(ImageAst2 , 'SendToBack');
   
   ImageAst3 := FormEkran.AddNewProImage(FormEkran , 'ImageAst3');
   ImageAst3.Align := alNone;
   ImageAst3.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst3.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst3 , '{"ImgUrl":"https://i.hizliresim.com/a3jouq4.png"}');
   ImageAst3.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst3.Position.Y := -200;
   ImageAst3.Visible := False;
   clRTMethod(ImageAst3 , 'SendToBack');
   
   ImageAst4 := FormEkran.AddNewProImage(FormEkran , 'ImageAst4');
   ImageAst4.Align := alNone;
   ImageAst4.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst4.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst4 , '{"ImgUrl":"https://i.hizliresim.com/6ctb2zg.png"}');
   ImageAst4.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst4.Position.Y := -200;
   ImageAst4.Visible := False;
   clRTMethod(ImageAst4 , 'SendToBack');
   
   ImageAst5 := FormEkran.AddNewProImage(FormEkran , 'ImageAst5');
   ImageAst5.Align := alNone;
   ImageAst5.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst5.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst5 , '{"ImgUrl":"https://i.hizliresim.com/amc7g1b.png"}');
   ImageAst5.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst5.Position.Y := -200;
   ImageAst5.Visible := False;
   clRTMethod(ImageAst5 , 'SendToBack');
   
   ImageAst6 := FormEkran.AddNewProImage(FormEkran , 'ImageAst6');
   ImageAst6.Align := alNone;
   ImageAst6.Width := TForm(FormEkran).ClientWidth / 8;
   ImageAst6.Height := TForm(FormEkran).ClientHeight / 16;
   clComponent.SetupComponent(ImageAst6 , '{"ImgUrl":"https://i.hizliresim.com/s3vn5i0.png"}');
   ImageAst6.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
   ImageAst6.Position.Y := -200;
   ImageAst6.Visible := False;
   clRTMethod(ImageAst6 , 'SendToBack');
  end;

  procedure AsteroidPositionChange //Asteroidlerin hareket olaylarını kontrol eden prosedür.
  begin
   if(ImageAst1.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
   begin
     ImageAst1.Position.Y := ImageAst1.Position.Y + 4;
   end;
   else
   begin
     ImageAst1.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
     ImageAst1.Position.Y := -200;
   end;
   
   if(ImageAst2.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
   begin
     ImageAst2.Position.Y := ImageAst2.Position.Y + 4;
   end;
   else
   begin
     ImageAst2.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
     ImageAst2.Position.Y := -200;
   end;
   
   if(ImageAst3.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
   begin
     ImageAst3.Position.Y := ImageAst3.Position.Y + 6;
   end;
   else
   begin
     ImageAst3.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
     ImageAst3.Position.Y := -200;
   end;
   
   if(ImageAst4.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
   begin
     ImageAst4.Position.Y := ImageAst4.Position.Y + 3;
   end;
   else
   begin
     ImageAst4.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
     ImageAst4.Position.Y := -200;
   end;
   

     if(ImageAst5.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
     begin
       ImageAst5.Position.Y := ImageAst5.Position.Y + 5;
     end;
     else
     begin
       ImageAst5.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
       ImageAst5.Position.Y := -200;
     end;
     if(ImageAst6.Position.Y <= (TForm(FormEkran).ClientHeight)-10 )then
     begin
       ImageAst6.Position.Y := ImageAst6.Position.Y + 4;
     end;
     else
     begin
       ImageAst6.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
       ImageAst6.Position.Y := -200;
      end;
  end;
  procedure YouDie;
  begin
    ButtonRestart.Visible := True;
    TimerGame.Enabled := False;
    TimerScore.Enabled := False;
    if(clomosy.GlobalVariableInteger = 1)then
    begin
      ImagePlayer1.Visible := False;
    end;
    else
    begin
      ImagePlayer1.Visible := False;
      ImagePlayer2.Visible := False;
    end;

    LabelScore.Visible := True;
    if(clomosy.GlobalVariableInteger = 1)then
    begin
      LabelScore.Text := 'SKORUNUZ : ' + IntToStr(score);
    end;
    MqttEkran.Send('Die');
  end;
  procedure CrashControl; //Asteroidlerin oyuncuya çarpıp çarpmadıklarını kontrol eden prosedür.
  begin
    if(Distance1 >= 10) and (Distance1 <= 50) or (Distance1 >= -60) and (Distance1 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance2 >= 10) and (Distance2 <= 50) or (Distance2 >= -60) and (Distance2 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance3 >= 10) and (Distance3 <= 50) or (Distance3 >= -60) and (Distance3 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance4 >= 10) and (Distance4 <= 50) or (Distance4 >= -60) and (Distance4 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance5 >= 10) and (Distance5 <= 50) or (Distance5 >= -60) and (Distance5 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance6 >= 10) and (Distance6 <= 50) or (Distance6 >= -60) and (Distance6 <= -20)then
    begin
      YouDie;
      if(clomosy.GlobalVariableInteger = 2)then
      LabelScore.Caption := 'Oyuncu 2 Kazandı';
      else
      LabelScore.Caption := 'Skorunuz : ' + IntToStr(score);
    end;
    if(Distance8 >= 10) and (Distance8 <= 50) or (Distance8 >= -60) and (Distance8 <= -20)then
    begin
      YouDie;
      LabelScore.Caption := 'Oyuncu 1 Kazandı';
    end;
    if(Distance9 >= 10) and (Distance9 <= 50) or (Distance9 >= -60) and (Distance9 <= -20) then
    begin
      YouDie;
      LabelScore.Caption := 'Oyuncu 1 Kazandı';
    end;
    if(Distance10 >= 10) and (Distance10 <= 50) or (Distance10 >= -60) and (Distance10 <= -20)then
    begin
      YouDie;
      LabelScore.Caption := 'Oyuncu 1 Kazandı';
    end;
    if(Distance11 >= 10) and (Distance11 <= 50) or (Distance11 >= -60) and (Distance11 <= -20) then
    begin
      YouDie;
      LabelScore.Caption := 'Oyuncu 1 Kazandı';
    end;
    if(Distance12 >= 10) and (Distance12 <= 50) or (Distance12 >= -60) and (Distance12 <= -20)then
    begin
      YouDie;
      LabelScore.Caption := 'Oyuncu 1 Kazandı';
    end;
  end;
  procedure StarPos;
  begin
    if(ImageStar1.Position.Y) <= (TForm(FormEkran).ClientHeight)then
    begin
      ImageStar1.Position.Y := ImageStar1.Position.Y + 1;
    end;
    else
    begin
      ImageStar1.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
      ImageStar1.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
      ImageStar1.Width := clMath.GenerateRandom(5,20);
      ImageStar1.Height := clMath.GenerateRandom(5,20);
    end;

    if(ImageStar2.Position.Y) <= (TForm(FormEkran).ClientHeight)then
    begin
      ImageStar2.Position.Y := ImageStar2.Position.Y + 2;
    end;
    else
    begin
      ImageStar2.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
      ImageStar2.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
      ImageStar2.Width := clMath.GenerateRandom(5,20);
      ImageStar2.Height := clMath.GenerateRandom(5,20);
    end;
    
    if(ImageStar3.Position.Y) <= (TForm(FormEkran).ClientHeight)then
    begin
      ImageStar3.Position.Y := ImageStar3.Position.Y + 4;
    end;
    else
    begin
      ImageStar3.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
      ImageStar3.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
      ImageStar3.Width := clMath.GenerateRandom(5,20);
      ImageStar3.Height := clMath.GenerateRandom(5,20);
    end;
    
    if(ImageStar4.Position.Y) <= (TForm(FormEkran).ClientHeight)then
    begin
      ImageStar4.Position.Y := ImageStar3.Position.Y + 3;
    end;
    else
    begin
      ImageStar4.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
      ImageStar4.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
      ImageStar4.Width := clMath.GenerateRandom(5,20);
      ImageStar4.Height := clMath.GenerateRandom(5,20);
    end;
    
    if(ImageStar5.Position.Y) <= (TForm(FormEkran).ClientHeight)then
    begin
      ImageStar5.Position.Y := ImageStar5.Position.Y +3;
    end;
    else
    begin
      ImageStar5.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
      ImageStar5.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
      ImageStar5.Width := clMath.GenerateRandom(5,20);
      ImageStar5.Height := clMath.GenerateRandom(5,20);
    end;
  end;

  procedure GameSpeed;
  begin
    if(score < 300)then
    begin
       TimerGame.Interval := 50;
    end;
    if(score >= 301) and (score <= 750)then
    begin
      TimerGame.Interval := 40;
    end;
    if(score >= 751) and (score <= 1000)then
    begin
      TimerGame.Interval := 35;
    end; 
    if(score >= 1001) and (score <= 1500)then
    begin
      TimerGame.Interval := 30;
    end; 
    if(score >= 1501) and (score <= 1750)then
    begin
      TimerGame.Interval := 25;
    end; 
    if(score >= 1751) and (score <= 2000)then
    begin
      TimerGame.Interval := 20;
    end; 
    if(score > 2000) and (score <= 2500)then
    begin
      TimerGame.Interval := 10;
    end; 
    if(score > 2500) and (score <= 3000)then
    begin
      TimerGame.Interval := 5;
    end; 
    if(score > 3000)then
    begin
      TimerGame.Interval := 1;
    end; 
   end;
  
  procedure RestartGame;
  begin
    score := 0;
    TimerScore.Enabled := True;
    TimerGame.Enabled := True;

    ImageAst1.Position.Y := -200;
    ImageAst2.Position.Y := -200;
    ImageAst3.Position.Y := -200;
    ImageAst4.Position.Y := -200;
    ImageAst5.Position.Y := -200;
    ImageAst6.Position.Y := -200;
    ImageAst2.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
    ImageAst3.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
    ImageAst4.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
    ImageAst5.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);
    ImageAst6.Position.X := clMath.GenerateRandom(50 , TForm(FormEkran).ClientWidth - 50);


    ButtonRestart.Visible := False;
    if (clomosy.GlobalVariableInteger = 1)then
    begin
      ImagePlayer1.Visible := True;
      ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 125;
    end;
    else if (clomosy.GlobalVariableInteger = 2)then
    begin
      ImagePlayer1.Visible := True;
      ImagePlayer2.Visible := True;
      ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 125;
      ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer2.Position.X := (TForm(FormEkran).ClientWidth / 2) - 25;
    end;
  end;
  
  procedure CloseFormClose;
  begin
    TClProButton(FormEkran.clFindComponent('BtnGoBack')).Click;
  end;
  
  procedure GameOperations;
  begin
    AsteroidPositionChange;
    CrashMeteor;
    CrashControl;
    GameSpeed;
    StarPos;
  end;
  
  procedure CreateEkran;
  begin
   //CREATE FORM
    FormEkran := TclGameForm.Create(Self);
    FormEkran.SetFormBGImage('https://i.hizliresim.com/ngg8s2l.jpg');
    score := 0;
    
    Player1 := '';
    Player2 := '';
    
    ButtonStartGame := FormEkran.AddNewProButton(FormEkran , 'ButtonStartGame' , 'BAŞLAT');
    ButtonStartGame.Align := alCenter;
    clComponent.SetupComponent(ButtonStartGame , '{"BackgroundColor":"null" , "BorderWidth":3 , "BorderColor":"#ffffff" , "RoundHeight":10 , "RoundWidth":10 , "TextBold":"yes" , "TextSize":20 , "TextColor":"#ffffff"}');
    ButtonStartGame.Width := TForm(FormEkran).ClientWidth / 2;
    ButtonStartGame.Height := TForm(FormEkran).ClientHeight / 8;
    clRTMethod(ButtonStartGame , 'BringTofront');
    ButtonStartGame.Margins.Bottom := 150;
    FormEkran.AddNewEvent(ButtonStartGame , tbeOnClick , 'Start');
    
   //CREATE BUTTON
    ButtonRestart := FormEkran.AddNewProButton(FormEkran , 'ButtonRestart' , 'RESTART');
    ButtonRestart.Align := alCenter;
    ButtonRestart.Width := TForm(FormEkran).ClientWidth / 2;
    ButtonRestart.Height := TForm(FormEkran).ClientHeight / 8;
    ButtonRestart.Visible := False;
    clComponent.SetupComponent(ButtonRestart , '{"BackgroundColor":"null" , "BorderWidth":3 , "BorderColor":"#ffffff" , "RoundHeight":10 , "RoundWidth":10 , "TextBold":"yes" , "TextSize":20 , "TextColor":"#ffffff"}');
    FormEkran.AddNewEvent(ButtonRestart , tbeOnClick , 'RestartGame');
    clRTMethod(ButtonRestart , 'BringTofront');
   
   //CREATE IMAGE
    //Oyuncular
    
    
    if(clomosy.GlobalVariableInteger = 1)then
    begin
      ImagePlayer1 := FormEkran.AddNewProImage(FormEkran , 'ImagePlayer1');
      ImagePlayer1.Align := alNone;
      ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 125;
      ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 7;
      ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 14;
      clComponent.SetupComponent(ImagePlayer1 , '{"ImgUrl":"https://i.hizliresim.com/r6jwvnc.png"}');
      
      LabelPlayer1 := FormEkran.AddNewProLabel(ImagePlayer1 , 'LabelPlayer1' , '');
      clComponent.SetupComponent(LabelPlayer1 , '{"TextColor":"#ffffff" , "TextBold":"yes" , "TextSize":20 , "TextHorizontalAlign":"center" , "TextVerticalAlign":"center"}');
      LabelPlayer1.Align := alCenter;
      LabelPlayer1.Visible := False;
      LabelPlayer1.Margins.Bottom := 80;
    end;
    else
    begin
      ImagePlayer1 := FormEkran.AddNewProImage(FormEkran , 'ImagePlayer1');
      ImagePlayer1.Align := alNone;
      ImagePlayer1.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer1.Position.X := (TForm(FormEkran).ClientWidth / 2) - 125;
      ImagePlayer1.Width := TForm(FormEkran).ClientWidth / 7;
      ImagePlayer1.Height := TForm(FormEkran).ClientHeight / 14;
      clComponent.SetupComponent(ImagePlayer1 , '{"ImgUrl":"https://i.hizliresim.com/r6jwvnc.png"}');
      
      ImagePlayer2 := FormEkran.AddNewProImage(FormEkran , 'ImagePlayer2');
      ImagePlayer2.Align := alNone;
      ImagePlayer2.Position.Y := TForm(FormEkran).ClientHeight - 75;
      ImagePlayer2.Position.X := (TForm(FormEkran).ClientWidth / 2) - 25;
      ImagePlayer2.Width := TForm(FormEkran).ClientWidth / 6;
      ImagePlayer2.Height := TForm(FormEkran).ClientHeight / 12;
      clComponent.SetupComponent(ImagePlayer2 , '{"ImgUrl":"https://i.hizliresim.com/kx3rqly.png"}');
      
      LabelPlayer1 := FormEkran.AddNewProLabel(ImagePlayer1 , 'LabelPlayer1' , '');
      clComponent.SetupComponent(LabelPlayer1 , '{"TextColor":"#ffffff" , "TextBold":"yes" , "TextSize":20 , "TextHorizontalAlign":"center" , "TextVerticalAlign":"center"}');
      LabelPlayer1.Align := alCenter;
      LabelPlayer1.Visible := False;
      LabelPlayer1.Margins.Bottom := 80;
      
      LabelPlayer2 := FormEkran.AddNewProLabel(ImagePlayer2 , 'LabelPlayer2' , 'Oyuncu 2');
      LabelPlayer2.Align := alCenter;
      LabelPlayer2.Margins.Bottom := 80;
      LabelPlayer2.Visible := False;
      clComponent.SetupComponent(LabelPlayer2 , '{"TextColor":"#ffffff" , "TextBold":"yes" , "TextSize":20 , "TextHorizontalAlign":"center" , "TextVerticalAlign":"center"}'); 
    end;

    

    
    ImageBtnBack := FormEkran.AddNewProImage(FormEkran , 'ImageBtnBack');
    ImageBtnBack.Align := alNone;
    clComponent.SetupComponent(ImageBtnBack , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/7945/7945195.png"}');
    FormEkran.AddNewEvent(ImageBtnBack , tbeOnClick , 'CloseFormClose');
    
    
    ImageStar1 := FormEkran.AddNewProImage(FormEkran , 'ImageStar1');
    ImageStar1.Width := clMath.GenerateRandom(5,20);
    ImageStar1.Height := clMath.GenerateRandom(5,20);
    ImageStar1.Align := alNone;
    ImageStar1.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
    ImageStar1.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
    clComponent.SetupComponent(ImageStar1 , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/4369/4369505.png"}');
    
    ImageStar2 := FormEkran.AddNewProImage(FormEkran , 'ImageStar2');
    ImageStar2.Width := clMath.GenerateRandom(5,20);
    ImageStar2.Height := clMath.GenerateRandom(5,20);
    ImageStar2.Align := alNone;
    ImageStar2.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
    ImageStar2.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
    clComponent.SetupComponent(ImageStar2 , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/753/753263.png"}');
    
    ImageStar3 := FormEkran.AddNewProImage(FormEkran , 'ImageStar3');
    ImageStar3.Width := clMath.GenerateRandom(5,20);
    ImageStar3.Height := clMath.GenerateRandom(5,20);
    ImageStar3.Align := alNone;
    ImageStar3.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
    ImageStar3.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
    clComponent.SetupComponent(ImageStar3 , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/5249/5249357.png"}');
    
    ImageStar4 := FormEkran.AddNewProImage(FormEkran , 'ImageStar4');
    ImageStar4.Width := clMath.GenerateRandom(5,20);
    ImageStar4.Height := clMath.GenerateRandom(5,20);
    ImageStar4.Align := alNone;
    ImageStar4.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
    ImageStar4.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
    clComponent.SetupComponent(ImageStar4 , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/10109/10109855.png"}');
    
    ImageStar5 := FormEkran.AddNewProImage(FormEkran , 'ImageStar5');
    ImageStar5.Width := clMath.GenerateRandom(5,20);
    ImageStar5.Height := clMath.GenerateRandom(5,20);
    ImageStar5.Align := alNone;
    ImageStar5.Position.Y := clMath.GenerateRandom(-2 * (TForm(FormEkran).ClientHeight),(-1 * TForm(FormEkran).ClientHeight));
    ImageStar5.Position.X := clMath.GenerateRandom(0 , TForm(FormEkran).ClientWidth - 30);
    clComponent.SetupComponent(ImageStar5 , '{"ImgUrl":"https://cdn-icons-png.flaticon.com/128/5249/5249357.png"}');
    
   
    
   //CREATE TİMER
    TimerGame := FormEkran.AddNewTimer(FormEkran , 'TimerGame' , 1);
    TimerGame.Enabled := False;
    FormEkran.AddNewEvent(TimerGame , tbeOnTimer , 'GameOperations');
    
    TimerScore := FormEkran.AddNewTimer(FormEkran , 'TimerScore' , 75);
    TimerScore.Enabled := False;
    FormEkran.AddNewEvent(TimerScore , tbeOnTimer , 'IncementScore');
  
    TimerResolutionGame := FormEkran.AddNewTimer(FormEkran , 'TimerResolutionGame' , 1);
    TimerResolutionGame.Enabled := True;
    FormEkran.AddNewEvent(TimerResolutionGame , tbeOnTimer , 'CtrlResolotuion');
  
   //CREATE LABEL
    LabelScore := FormEkran.AddNewProLabel(FormEkran , 'LabelScore' , '0');
   // LabelScore.Visible := False;
    LabelScore.Align := alTop;
    LabelScore.Width := TForm(FormEkran).ClientWidth / 2.5;
    LabelScore.Height := TForm(FormEkran).ClientHeight / 10;
    clComponent.SetupComponent(LabelScore , '{"TextColor":"#ffffff" , "TextSize":25 , "TextBold":"yes","TextVerticalAlign" : "center" , "TextHorizontalAlign":"center" }');
    clRTMethod(LabelScore , 'SendToBack');
  
    LabelDurum:= FormEkran.AddNewProLabel(FormEkran , 'LabelDurum' , 'Connected');
    LabelDurum.Align := alNone;
    LabelDurum.Visible := True;
    clComponent.SetupComponent(LabelDurum , '{"TextColor":"#952323" , "TextBold":"yes" , "TextSize":15 , "TextVerticalAlign" : "center" , "TextHorizontalAlign":"center"}');
  
    MqttEkran := FormEkran.AddNewMQTTConnection(FormEkran , 'MqttEkran');
    FormEkran.AddNewEvent(MqttEkran , tbeOnMQTTStatusChanged , 'StatusChanged');
    FormEkran.AddNewEvent(MqttEkran , tbeOnMQTTPublishReceived , 'PublisStatut');
    MqttEkran.Channel := EditPasword.Text;
    MqttEkran.Connect;
    
    LabelPassword := FormEkran.AddNewProLabel(FormEkran , 'LabelPassword' ,'');
    LabelPassword.Width := TForm(FormEkran).ClientWidth;
    LabelPassword.Visible := True;
    LabelPassword.Align := alCenter;
    LabelPassword.Height := TForm(FormEkran).ClientHeight / 7;
    LabelPassword.Caption := 'ŞİFRENİZ : ' + quotedStr(MqttEkran.Channel) + ' OYUNCU BEKLENİYOR';
    clComponent.SetupComponent(LabelPassword , '{"TextColor":"#ffffff" , "TextSize":17 , "TextBold":"yes","TextVerticalAlign" : "center" , "TextHorizontalAlign":"center" }');

  
    //FormEkran.AddGameAssetFromUrl('https://www.clomosy.com/game/assets/Explosion.png');
    //FormEkran.AnimationWidth := 75; 
    //FormEkran.AnimationHeight := 75;
    //FormEkran.clAnimateBitmap.AnimationCount :=9;
    //FormEkran.clAnimateBitmap.AnimationRowCount:=3;
    //FormEkran.clAnimateBitmap.Delay := 0; 
    //FormEkran.clAnimateBitmap.Duration := 2;
  
  

  
 
  CreateAsteroid;
   FormEkran.Run;
  end;
  
  
  begin
    if(Clomosy.GlobalVariableString = 'Ekran')then
    begin
      CreateEkran;
      if (Clomosy.GlobalVariableInteger = 1) then
      begin 
        LabelScore.Visible := True;
      end;
    end;
    else
    begin
      CreateKol;
    end;
  
  end;
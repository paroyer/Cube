# Cube

My Cheat Engine Trainer if ever it could be usefull to you, flag as a virus by windows defender since it's a tool that modify memory value.

Here's the source code:

--Form
function round(num, numDecimalPlaces)
  return tonumber(string.format("%." .. (numDecimalPlaces or 0) .. "f", num))
end
function setbit(address, bitnr, state)
  if (bitnr>7) then error('setbit only works for byte sizes. rewrite this for bigger values') end
  b=readInteger(address)
  if (state==1) then
    b=b | (1<<bitnr)
  else
    b=b & ~(1<<bitnr)
  end
  writeInteger(address,b)
end
--errorOnLookupFailure(false)
settings=getSettings('mytrainerstuff')
PathTest= settings.Value['Path']
ActualPath= PathTest:gsub("\\","\\\\")
setProperty(UDF1_CEComboBox1, 'ItemIndex', 0)
RaceModelToLaunchHead = settings.Value['RaceModelToLaunchHead']
RaceModelToLaunchBody = settings.Value['RaceModelToLaunchBody']
RaceModelToLaunchHand = settings.Value['RaceModelToLaunchHand']
RaceModelToLaunchFeet = settings.Value['RaceModelToLaunchFeet']
RaceModelToLaunchHair = settings.Value['RaceModelToLaunchHair']
RaceModelToLaunchShoulders = settings.Value['RaceModelToLaunchShoulders']
RaceModelToLaunchBack = settings.Value['RaceModelToLaunchBack']
RaceModelToLaunchWings = settings.Value['RaceModelToLaunchWings']
function UDF1_CEButton5Click(sender)
settings.Value['RaceModelToLaunchHead'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90")--Head
settings.Value['RaceModelToLaunchBody'] = ReadSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98")--Body
settings.Value['RaceModelToLaunchHand'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94")--Hand
settings.Value['RaceModelToLaunchFeet'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96")--Feet
settings.Value['RaceModelToLaunchHair'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92")--Hair
settings.Value['RaceModelToLaunchShoulders'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C")--Shoulders
settings.Value['RaceModelToLaunchBack'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A")--Back
settings.Value['RaceModelToLaunchWings'] = ReadSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E")--Wings
RaceModelToLaunchHead = settings.Value['RaceModelToLaunchHead']
RaceModelToLaunchBody = settings.Value['RaceModelToLaunchBody']
RaceModelToLaunchHand = settings.Value['RaceModelToLaunchHand']
RaceModelToLaunchFeet = settings.Value['RaceModelToLaunchFeet']
RaceModelToLaunchHair = settings.Value['RaceModelToLaunchHair']
RaceModelToLaunchShoulders = settings.Value['RaceModelToLaunchShoulders']
RaceModelToLaunchBack = settings.Value['RaceModelToLaunchBack']
RaceModelToLaunchWings = settings.Value['RaceModelToLaunchWings']
end
form_show(UDF1)
addresslist=getAddressList()
getAutoAttachList().add("cubeworld.exe")
function UDF1_CEButton2Click(sender)
 openProcess('cubeworld.exe')
end
function CloseClick()
autoAssemble([[
  MobDmgAOB:
  db F3 0F 5C 47 20
  unregistersymbol(MobDmgAOB)
  dealloc(newmem)
  ]])--BeSureToRevertAAchanges
  closeCE()
  return caFree
end
UDF1.OnClose = CloseClick

--TrainerIcon
local int = getInternet()
local ICO = int.getURL("https://www.beprosoftware.com/wp-content/uploads/2013/06/woocube.png")
local IM = createStringStream(ICO)
int.Destroy()
getApplication().Icon = ICO
function attachIcon(frm,tblFile)
  local p = createPicture()
  p.loadFromStream(tblFile)
  local b = p.getBitmap()
  frm.Icon = b
  getApplication().Icon = b
  frm.ShowInTaskBar='stAlways'
end
attachIcon(UDF1,IM)
UDF1.show()

--About
AboutTitle=[[Cubeworld Cheat Engine Trainer Test]]
AboutText=[[Made by Philrd]]
about = createForm(false)
about.Caption='About'
about.CenterScreen()
about.Height = 250
about.Width = 300
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(about, [[About.png]])
aboutGitButton = createButton(about)
aboutGitButton.Left = 10
aboutGitButton.Top = 200
aboutGitButton.Width = 100
aboutGitButton.Height = 40
aboutGitButton.Caption = 'Github Link'
aboutGitButton.onClick = openGit
aboutGuideButton = createButton(about)
aboutGuideButton.Left = 190
aboutGuideButton.Top = 200
aboutGuideButton.Width = 100
aboutGuideButton.Height = 40
aboutGuideButton.Caption = 'Help'
aboutGuideButton.onClick = openGuide
aboutlabel=createLabel(about)
aboutlabel.setCaption(AboutText)
aboutlabel.Top = 20
aboutlabel.Left = 20
aboutlabel.Font.Size = 10
--aboutlabel.Font.Style = ('fsUnderline, fsBold')
--aboutlabel.Font.Color = 0xffffff
labelTitle=createLabel(about)
labelTitle.setCaption(AboutTitle)
labelTitle.Top = 0
labelTitle.Left = 10
labelTitle.Font.Size = 12
labelTitle.Font.Style = ('fsUnderline, fsBold')
--labelTitle.Font.Color = 0xffffff
function openGit()
 shellExecute('https://github.com/paroyer.html')
end
function openGuide()
 shellExecute('https://imgur.com/a/9m7Pu3m')
end
function UDF1_CEButton1Click(sender)
about.show()
end
about.OnClose = function(sender)
return caHide
end

--Hair ToggleBox
function UDF1_CEToggleBox1Change(sender)
  if(checkbox_getState(UDF1.CEToggleBox1) == 1) then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92",-1)
hairt = createTimer(getMainForm())
hairt.Interval = 50
hairt.OnTimer = function(sender)
 writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92",-1) end
  else
hairt.destroy()
  end
end

--Favorite TrackBar
function UDF1_CEButton3Click(sender)
 setProperty(UDF1_CETrackBar1, 'position', (tonumber(UDF1_CETrackBar1.position)-1))
end
function UDF1_CEButton4Click(sender)
 setProperty(UDF1_CETrackBar1, 'position', (tonumber(UDF1_CETrackBar1.position)+1))
end
function UDF1_CEComboBox1Change(sender)
 setProperty(UDF1_CETrackBar1, 'Position',UDF1_CEComboBox1.ItemIndex)
 end
function UDF1_CETrackBar1Change(sender)
 setProperty(UDF1_CEComboBox1, 'ItemIndex',UDF1_CETrackBar1.position)
 if UDF1_CEComboBox1.ItemIndex == 1 then
 setProperty(slider, 'Position', settings.Value['Mainedit'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8'])
 setProperty(BSedit, 'Position', settings.Value['BSedit'])
 setProperty(BSedit2, 'Position', settings.Value['BSedit2'])
 setProperty(BSedit3, 'Position', settings.Value['BSedit3'])
 setProperty(BSedit4, 'Position', settings.Value['BSedit4'])
 setProperty(BSedit5, 'Position', settings.Value['BSedit5'])
 setProperty(BSedit6, 'Position', settings.Value['BSedit6'])
 setProperty(BSedit7, 'Position', settings.Value['BSedit7'])
 setProperty(BSedit8, 'Position', settings.Value['BSedit8'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3'])
 elseif UDF1_CEComboBox1.ItemIndex == 2 then
 setProperty(slider, 'Position', settings.Value['Mainedit-1'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-1'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-1'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-1'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-1'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-1'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-1'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-1'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-1'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-1'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-1'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-1'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-1'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-1'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-1'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-1'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-1'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-1'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-1'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-1'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-1'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-1'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-1'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-1'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-1'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-1'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-1'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-1'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-1'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-1'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-1'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-1'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-1'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-1'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-1'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-1'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-1'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-1'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-1'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-1'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-1'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-1'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-1'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-1'])
 elseif UDF1_CEComboBox1.ItemIndex == 3 then
 setProperty(slider, 'Position', settings.Value['Mainedit-2'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-2'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-2'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-2'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-2'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-2'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-2'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-2'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-2'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-2'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-2'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-2'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-2'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-2'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-2'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-2'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-2'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-2'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-2'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-2'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-2'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-2'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-2'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-2'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-2'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-2'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-2'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-2'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-2'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-2'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-2'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-2'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-2'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-2'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-2'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-2'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-2'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-2'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-2'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-2'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-2'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-2'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-2'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-2'])
  elseif UDF1_CEComboBox1.ItemIndex == 4 then
 setProperty(slider, 'Position', settings.Value['Mainedit-3'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-3'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-3'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-3'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-3'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-3'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-3'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-3'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-3'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-3'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-3'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-3'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-3'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-3'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-3'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-3'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-3'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-3'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-3'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-3'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-3'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-3'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-3'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-3'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-3'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-3'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-3'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-3'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-3'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-3'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-3'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-3'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-3'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-3'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-3'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-3'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-3'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-3'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-3'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-3'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-3'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-3'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-3'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-3'])
 elseif UDF1_CEComboBox1.ItemIndex == 5 then
 setProperty(slider, 'Position', settings.Value['Mainedit-4'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-4'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-4'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-4'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-4'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-4'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-4'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-4'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-4'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-4'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-4'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-4'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-4'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-4'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-4'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-4'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-4'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-4'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-4'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-4'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-4'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-4'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-4'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-4'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-4'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-4'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-4'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-4'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-4'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-4'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-4'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-4'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-4'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-4'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-4'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-4'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-4'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-4'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-4'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-4'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-4'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-4'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-4'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-4'])
elseif UDF1_CEComboBox1.ItemIndex == 6 then
 setProperty(slider, 'Position', settings.Value['Mainedit-5'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-5'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-5'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-5'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-5'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-5'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-5'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-5'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-5'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-5'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-5'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-5'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-5'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-5'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-5'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-5'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-5'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-5'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-5'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-5'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-5'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-5'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-5'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-5'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-5'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-5'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-5'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-5'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-5'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-5'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-5'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-5'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-5'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-5'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-5'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-5'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-5'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-5'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-5'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-5'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-5'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-5'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-5'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-5'])
elseif UDF1_CEComboBox1.ItemIndex == 7 then
 setProperty(slider, 'Position', settings.Value['Mainedit-6'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-6'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-6'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-6'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-6'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-6'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-6'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-6'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-6'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-6'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-6'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-6'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-6'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-6'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-6'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-6'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-6'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-6'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-6'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-6'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-6'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-6'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-6'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-6'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-6'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-6'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-6'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-6'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-6'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-6'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-6'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-6'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-6'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-6'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-6'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-6'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-6'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-6'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-6'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-6'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-6'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-6'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-6'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-6'])
elseif UDF1_CEComboBox1.ItemIndex == 8 then
 setProperty(slider, 'Position', settings.Value['Mainedit-7'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-7'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-7'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-7'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-7'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-7'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-7'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-7'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-7'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-7'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-7'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-7'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-7'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-7'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-7'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-7'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-7'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-7'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-7'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-7'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-7'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-7'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-7'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-7'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-7'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-7'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-7'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-7'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-7'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-7'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-7'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-7'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-7'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-7'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-7'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-7'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-7'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-7'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-7'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-7'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-7'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-7'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-7'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-7'])
elseif UDF1_CEComboBox1.ItemIndex == 9 then
 setProperty(slider, 'Position', settings.Value['Mainedit-8'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-8'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-8'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-8'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-8'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-8'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-8'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-8'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-8'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-8'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-8'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-8'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-8'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-8'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-8'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-8'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-8'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-8'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-8'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-8'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-8'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-8'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-8'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-8'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-8'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-8'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-8'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-8'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-8'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-8'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-8'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-8'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-8'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-8'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-8'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-8'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-8'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-8'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-8'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-8'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-8'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-8'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-8'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-8'])
 elseif UDF1_CEComboBox1.ItemIndex == 10 then
 setProperty(slider, 'Position', settings.Value['Mainedit-9'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-9'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-9'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-9'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-9'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-9'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-9'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-9'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-9'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-9'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-9'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-9'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-9'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-9'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-9'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-9'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-9'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-9'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-9'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-9'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-9'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-9'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-9'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-9'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-9'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-9'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-9'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-9'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-9'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-9'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-9'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-9'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-9'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-9'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-9'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-9'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-9'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-9'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-9'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-9'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-9'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-9'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-9'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-9'])
 elseif UDF1_CEComboBox1.ItemIndex == 11 then
 setProperty(slider, 'Position', settings.Value['Mainedit-10'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-10'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-10'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-10'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-10'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-10'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-10'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-10'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-10'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-10'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-10'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-10'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-10'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-10'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-10'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-10'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-10'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-10'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-10'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-10'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-10'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-10'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-10'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-10'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-10'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-10'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-10'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-10'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-10'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-10'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-10'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-10'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-10'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-10'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-10'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-10'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-10'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-10'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-10'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-10'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-10'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-10'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-10'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-10'])
 elseif UDF1_CEComboBox1.ItemIndex == 12 then
 setProperty(slider, 'Position', settings.Value['Mainedit-11'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-11'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-11'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-11'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-11'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-11'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-11'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-11'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-11'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-11'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-11'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-11'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-11'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-11'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-11'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-11'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-11'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-11'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-11'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-11'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-11'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-11'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-11'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-11'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-11'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-11'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-11'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-11'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-11'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-11'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-11'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-11'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-11'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-11'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-11'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-11'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-11'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-11'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-11'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-11'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-11'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-11'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-11'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-11'])
 elseif UDF1_CEComboBox1.ItemIndex == 13 then
 setProperty(slider, 'Position', settings.Value['Mainedit-12'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-12'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-12'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-12'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-12'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-12'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-12'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-12'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-12'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-12'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-12'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-12'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-12'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-12'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-12'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-12'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-12'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-12'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-12'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-12'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-12'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-12'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-12'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-12'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-12'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-12'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-12'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-12'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-12'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-12'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-12'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-12'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-12'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-12'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-12'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-12'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-12'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-12'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-12'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-12'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-12'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-12'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-12'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-12'])
 elseif UDF1_CEComboBox1.ItemIndex == 14 then
 setProperty(slider, 'Position', settings.Value['Mainedit-13'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-13'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-13'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-13'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-13'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-13'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-13'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-13'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-13'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-13'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-13'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-13'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-13'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-13'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-13'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-13'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-13'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-13'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-13'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-13'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-13'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-13'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-13'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-13'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-13'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-13'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-13'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-13'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-13'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-13'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-13'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-13'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-13'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-13'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-13'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-13'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-13'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-13'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-13'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-13'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-13'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-13'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-13'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-13'])
 elseif UDF1_CEComboBox1.ItemIndex == 15 then
 setProperty(slider, 'Position', settings.Value['Mainedit-14'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-14'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-14'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-14'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-14'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-14'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-14'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-14'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-14'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-14'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-14'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-14'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-14'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-14'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-14'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-14'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-14'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-14'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-14'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-14'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-14'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-14'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-14'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-14'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-14'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-14'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-14'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-14'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-14'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-14'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-14'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-14'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-14'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-14'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-14'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-14'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-14'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-14'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-14'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-14'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-14'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-14'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-14'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-14'])
 elseif UDF1_CEComboBox1.ItemIndex == 16 then
 setProperty(slider, 'Position', settings.Value['Mainedit-15'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-15'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-15'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-15'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-15'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-15'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-15'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-15'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-15'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-15'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-15'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-15'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-15'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-15'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-15'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-15'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-15'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-15'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-15'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-15'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-15'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-15'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-15'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-15'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-15'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-15'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-15'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-15'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-15'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-15'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-15'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-15'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-15'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-15'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-15'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-15'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-15'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-15'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-15'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-15'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-15'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-15'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-15'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-15'])
 elseif UDF1_CEComboBox1.ItemIndex == 17 then
 setProperty(slider, 'Position', settings.Value['Mainedit-16'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-16'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-16'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-16'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-16'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-16'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-16'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-16'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-16'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-16'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-16'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-16'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-16'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-16'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-16'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-16'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-16'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-16'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-16'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-16'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-16'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-16'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-16'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-16'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-16'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-16'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-16'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-16'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-16'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-16'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-16'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-16'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-16'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-16'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-16'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-16'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-16'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-16'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-16'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-16'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-16'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-16'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-16'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-16'])
 elseif UDF1_CEComboBox1.ItemIndex == 18 then
 setProperty(slider, 'Position', settings.Value['Mainedit-17'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-17'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-17'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-17'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-17'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-17'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-17'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-17'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-17'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-17'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-17'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-17'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-17'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-17'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-17'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-17'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-17'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-17'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-17'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-17'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-17'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-17'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-17'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-17'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-17'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-17'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-17'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-17'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-17'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-17'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-17'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-17'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-17'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-17'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-17'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-17'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-17'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-17'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-17'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-17'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-17'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-17'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-17'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-17'])
 elseif UDF1_CEComboBox1.ItemIndex == 19 then
 setProperty(slider, 'Position', settings.Value['Mainedit-18'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-18'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-18'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-18'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-18'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-18'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-18'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-18'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-18'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-18'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-18'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-18'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-18'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-18'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-18'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-18'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-18'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-18'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-18'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-18'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-18'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-18'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-18'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-18'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-18'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-18'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-18'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-18'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-18'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-18'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-18'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-18'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-18'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-18'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-18'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-18'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-18'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-18'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-18'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-18'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-18'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-18'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-18'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-18'])
 elseif UDF1_CEComboBox1.ItemIndex == 20 then
 setProperty(slider, 'Position', settings.Value['Mainedit-19'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-19'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-19'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-19'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-19'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-19'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-19'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-19'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-19'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-19'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-19'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-19'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-19'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-19'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-19'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-19'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-19'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-19'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-19'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-19'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-19'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-19'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-19'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-19'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-19'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-19'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-19'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-19'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-19'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-19'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-19'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-19'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-19'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-19'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-19'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-19'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-19'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-19'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-19'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-19'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-19'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-19'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-19'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-19'])
 end
end
--PetForm
local petForm = createForm(false)
petForm.Caption='Pet'
petForm.Height = 150
petForm.Top = 380
petForm.Left = 340
petForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox2, 0)
   return caHide
end
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(petForm, [[bgpetlist.png]])
sliderPet=createTrackBar(petForm)
sliderPet.Width = 270
sliderPet.Height = 25
sliderPet.Left = 25
sliderPet.Top = 105
sliderPet.Max = 306
sliderPet.Min = -1
setProperty(sliderPet, 'Position', -1)
PetModelButton=createToggleBox(petForm)
PetModelButton.caption = 'Model'
PetModelButton.Width = 50
PetModelButton.Height = 15
PetModelButton.Top = 132
PetModelButton.Left = 250
sliderButton1=createButton(petForm)
sliderButton1.caption = '<'
sliderButton1.Width = 25
sliderButton1.Height = 25
sliderButton1.Top = 105
sliderButton1.Left = 5
sliderButton1.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)-1))
end
sliderButton2=createButton(petForm)
sliderButton2.caption = '>'
sliderButton2.Width = 25
sliderButton2.Height = 25
sliderButton2.Top = 105
sliderButton2.Left = 290
sliderButton2.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)+1))
end
x5Button1=createButton(petForm)
x5Button1.caption = '>>'
x5Button1.Width = 25
x5Button1.Height = 25
x5Button1.Top = 80
x5Button1.Left = 265
x5Button1.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)+5))
end
x5Button2=createButton(petForm)
x5Button2.caption = '<<'
x5Button2.Width = 25
x5Button2.Height = 25
x5Button2.Top = 80
x5Button2.Left = 30
x5Button2.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)-5))
end
x10Button1=createButton(petForm)
x10Button1.caption = '<<<'
x10Button1.Width = 25
x10Button1.Height = 25
x10Button1.Top = 80
x10Button1.Left = 5
x10Button1.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)-10))
end
x10Button2=createButton(petForm)
x10Button2.caption = '>>>'
x10Button2.Width = 25
x10Button2.Height = 25
x10Button2.Top = 80
x10Button2.Left = 290
x10Button2.OnClick = function(sender)
sliderPet.position=((tonumber(sliderPet.Position)+10))
end
edit=createEdit(petForm)
edit.Top = 80
edit.Left = 125
edit.Width = 75
edit2=createEdit(petForm)
edit2.visible=false
edit2.Top = 80
edit2.Left = 125
edit2.Width = 75
setButton=createButton(petForm)
setButton.Width = 30
setButton.Height = 20
setButton.Caption = 'Set'
setButton.Top = 82
setButton.Left = 95
editRefreshTimer = createTimer(getMainForm())
editRefreshTimer.Interval = 500
editRefreshTimer.onTimer = function(sender)
  if edit.text == readInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8BC") then
  else
  setProperty(edit, 'text', readInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8BC"))
 end
end
--*EditBoxChangeValueOnSetButton*--
setMethodProperty(edit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and (keynr~=110) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
function setButton.OnClick(sender)
 if edit2.visible == true then
 edit2.visible=false
 setProperty(slider, 'Position', getProperty(edit2, 'text'))
 elseif edit2.visible == false then
 edit2.visible=true
 setProperty(edit2, 'Text', nil)
 end
end
--*Actual value send/get*--
sliderPet.OnChange = function(sender)
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8BC", getProperty(sliderPet, 'Position'))
end
sliderPetRefreshTimer = createTimer(getMainForm())
sliderPetRefreshTimer.Interval = 500
sliderPetRefreshTimer.onTimer = function(sender)
  if sliderPet.position == readInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8BC") then
  else
  setProperty(sliderPet, 'Position', readInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8BC"))
 end
end
--PetToggleButton OnMainForm
function UDF1_CEToggleBox2Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox2) == 1) then
petForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox2) == 0) then
petForm.hide()
  end
end
--PetModelForm
local PetModelForm = createForm(false)
PetModelForm.Caption='Pet Model'
PetModelForm.Height = 500
PetModelForm.Width = 400
PetModelForm.Top = 450
PetModelForm.Left = 450
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(PetModelForm, [[ModelFormMain.png]])
PetPresetComboBox = createComboBox(PetModelForm)
PetPresetComboBox.Width = 100
PetPresetComboBox.top = 450
PetPresetComboBox.left = 150
PetPresetComboBoxitem = PetPresetComboBox.getItems
PetPresetComboBox.style = 'csDropDownList'
PetPresetComboBox.items.add("Preset: 1")
PetPresetComboBox.items.add("Preset: 2")
PetPresetComboBox.items.add("Preset: 3")
PetPresetComboBox.items.add("Preset: 4")
PetPresetComboBox.items.add("Preset: 5")
PetPresetComboBox.items.add("Preset: 6")
PetPresetComboBox.items.add("Preset: 7")
PetPresetComboBox.items.add("Preset: 8")
PetPresetComboBox.items.add("Preset: 9")
PetPresetComboBox.items.add("Preset: 10")
PetPresetSaveButton = createButton(PetModelForm)
PetPresetSaveButton.top = 452
PetPresetSaveButton.Caption = 'Save'
PetPresetSaveButton.Width = 30
PetPresetSaveButton.Height = 20
PetPresetSaveButton.left = 110
PetPresetSaveButton.OnClick = function (sender)
 if PetPresetComboBox.ItemIndex == 0 then
settings.Value['PetMainedit'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 1 then
settings.Value['PetMainedit-1'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-1'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-1'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-1'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-1'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-1'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-1'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-1'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-1'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-1'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-1'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-1'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-1'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-1'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-1'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-1'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-1'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-1'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-1'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-1'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-1'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-1'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-1'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-1'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-1'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-1'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-1'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-1'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-1'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-1'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-1'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-1'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-1'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-1'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-1'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-1'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-1'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-1'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-1'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-1'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-1'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-1'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-1'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-1'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 2 then
settings.Value['PetMainedit-2'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-2'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-2'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-2'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-2'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-2'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-2'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-2'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-2'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-2'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-2'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-2'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-2'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-2'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-2'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-2'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBRedit2-2'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-2'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-2'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-2'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-2'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-2'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-2'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-2'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-2'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-2'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-2'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-2'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-2'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-2'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-2'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-2'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-2'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-2'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-2'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-2'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-2'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-2'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-2'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-2'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-2'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-2'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-2'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-2'] = getProperty(PPetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 3 then
settings.Value['PetMainedit-3'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-3'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-3'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-3'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-3'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-3'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-3'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-3'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-3'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-3'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-3'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-3'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-3'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-3'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-3'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-3'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-3'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-3'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-3'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-3'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-3'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-3'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-3'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-3'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-3'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-3'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-3'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-3'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-3'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-3'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-3'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-3'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-3'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-3'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-3'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-3'] = getProperty(PetBPeditZ2, 'Position')
settings.Value['PetBPeditZ3-3'] = getProperty(PetBPeditZ3, 'Position')
settings.Value['PetBPeditZ4-3'] = getProperty(PetBPeditZ4, 'Position')
settings.Value['PetBPeditZ5-3'] = getProperty(PetBPeditZ5, 'Position')
settings.Value['PetBPeditZ6-3'] = getProperty(PetBPeditZ6, 'Position')
settings.Value['PetBPeditZ7-3'] = getProperty(PetBPeditZ7, 'Position')
settings.Value['PetHBedit-3'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-3'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-3'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 4 then
settings.Value['PetMainedit-4'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-4'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-4'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-4'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-4'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-4'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-4'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-4'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-4'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-4'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-4'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-4'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-4'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-4'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-4'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-4'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-4'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-4'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-4'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-4'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-4'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-4'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-4'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-4'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-4'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-4'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-4'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-4'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-4'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-4'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-4'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-4'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-4'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-4'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-4'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-4'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-4'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-4'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-4'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-4'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-4'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-4'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-4'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-4'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 5 then
settings.Value['PetMainedit-5'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-5'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-5'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-5'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-5'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-5'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-5'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-5'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-5'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-5'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-5'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-5'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-5'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-5'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-5'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-5'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-5'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-5'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-5'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-5'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-5'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-5'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-5'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-5'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-5'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-5'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-5'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-5'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-5'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-5'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-5'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-5'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-5'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-5'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-5'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-5'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-5'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-5'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-5'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-5'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-5'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-5'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-5'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-5'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 6 then
settings.Value['PetMainedit-6'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-6'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-6'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-6'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-6'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-6'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-6'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-6'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-6'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-6'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-6'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-6'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-6'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-6'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-6'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-6'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-6'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-6'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-6'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-6'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-6'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-6'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-6'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-6'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-6'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-6'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-6'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-6'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-6'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-6'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-6'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-6'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-6'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-6'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-6'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-6'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-6'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-6'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-6'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-6'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-6'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-6'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-6'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-6'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 7 then
settings.Value['PetMainedit-7'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-7'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-7'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-7'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-7'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-7'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-7'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-7'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-7'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-7'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-7'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-7'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-7'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-7'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-7'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-7'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-7'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-7'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-7'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-7'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-7'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-7'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-7'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-7'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-7'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-7'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-7'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-7'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-7'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-7'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-7'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-7'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-7'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-7'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-7'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-7'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-7'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-7'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-7'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-7'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-7'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-7'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-7'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-7'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 8 then
settings.Value['PetMainedit-8'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-8'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-8'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-8'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-8'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-8'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-8'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-8'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-8'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-8'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-8'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-8'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-8'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-8'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-8'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-8'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-8'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-8'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-8'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-8'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-8'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-8'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-8'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-8'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-8'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-8'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-8'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-8'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-8'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-8'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-8'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-8'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-8'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-8'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-8'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-8'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-8'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-8'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-8'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-8'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-8'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-8'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-8'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-8'] = getProperty(PetsliderHB3, 'Position')
 elseif PetPresetComboBox.ItemIndex == 9 then
settings.Value['PetMainedit-9'] = getProperty(PetMainedit, 'text')
settings.Value['PetMainedit2-9'] = getProperty(PetMainedit2, 'text')
settings.Value['PetMainedit3-9'] = getProperty(PetMainedit3, 'text')
settings.Value['PetMainedit4-9'] = getProperty(PetMainedit4, 'text')
settings.Value['PetMainedit5-9'] = getProperty(PetMainedit5, 'text')
settings.Value['PetMainedit6-9'] = getProperty(PetMainedit6, 'text')
settings.Value['PetMainedit7-9'] = getProperty(PetMainedit7, 'text')
settings.Value['PetMainedit8-9'] = getProperty(PetMainedit8, 'text')
settings.Value['PetBSedit-9'] = getProperty(PetsliderBS, 'Position')
settings.Value['PetBSedit2-9'] = getProperty(PetsliderBS2, 'Position')
settings.Value['PetBSedit3-9'] = getProperty(PetsliderBS3, 'Position')
settings.Value['PetBSedit4-9'] = getProperty(PetsliderBS4, 'Position')
settings.Value['PetBSedit5-9'] = getProperty(PetsliderBS5, 'Position')
settings.Value['PetBSedit6-9'] = getProperty(PetsliderBS6, 'Position')
settings.Value['PetBSedit7-9'] = getProperty(PetsliderBS7, 'Position')
settings.Value['PetBSedit8-9'] = getProperty(PetsliderBS8, 'Position')
settings.Value['PetBRedit2-9'] = getProperty(PetBRedit2, 'text')
settings.Value['PetBRedit3-9'] = getProperty(PetBRedit3, 'text')
settings.Value['PetBRedit4-9'] = getProperty(PetBRedit4, 'text')
settings.Value['PetBRedit5-9'] = getProperty(PetBRedit5, 'text')
settings.Value['PetBRedit6-9'] = getProperty(PetBRedit6, 'text')
settings.Value['PetBRedit7-9'] = getProperty(PetBRedit7, 'text')
settings.Value['PetBRedit8-9'] = getProperty(PetBRedit8, 'text')
settings.Value['PetBPeditX2-9'] = getProperty(PetsliderBPX2, 'Position')
settings.Value['PetBPeditX3-9'] = getProperty(PetsliderBPX3, 'Position')
settings.Value['PetBPeditX4-9'] = getProperty(PetsliderBPX4, 'Position')
settings.Value['PetBPeditX5-9'] = getProperty(PetsliderBPX5, 'Position')
settings.Value['PetBPeditX6-9'] = getProperty(PetsliderBPX6, 'Position')
settings.Value['PetBPeditX7-9'] = getProperty(PetsliderBPX7, 'Position')
settings.Value['PetBPeditY2-9'] = getProperty(PetsliderBPY2, 'Position')
settings.Value['PetBPeditY3-9'] = getProperty(PetsliderBPY3, 'Position')
settings.Value['PetBPeditY4-9'] = getProperty(PetsliderBPY4, 'Position')
settings.Value['PetBPeditY5-9'] = getProperty(PetsliderBPY5, 'Position')
settings.Value['PetBPeditY6-9'] = getProperty(PetsliderBPY6, 'Position')
settings.Value['PetBPeditY7-9'] = getProperty(PetsliderBPY7, 'Position')
settings.Value['PetBPeditZ2-9'] = getProperty(PetsliderBPZ2, 'Position')
settings.Value['PetBPeditZ3-9'] = getProperty(PetsliderBPZ3, 'Position')
settings.Value['PetBPeditZ4-9'] = getProperty(PetsliderBPZ4, 'Position')
settings.Value['PetBPeditZ5-9'] = getProperty(PetsliderBPZ5, 'Position')
settings.Value['PetBPeditZ6-9'] = getProperty(PetsliderBPZ6, 'Position')
settings.Value['PetBPeditZ7-9'] = getProperty(PetsliderBPZ7, 'Position')
settings.Value['PetHBedit-9'] = getProperty(PetsliderHB, 'Position')
settings.Value['PetHBedit2-9'] = getProperty(PetsliderHB2, 'Position')
settings.Value['PetHBedit3-9'] = getProperty(PetsliderHB3, 'Position')
 end
end
PetPresetLoadButton = createButton(PetModelForm)
PetPresetLoadButton.top = 452
PetPresetLoadButton.Caption = 'Load'
PetPresetLoadButton.Width = 30
PetPresetLoadButton.Height = 20
PetPresetLoadButton.left = 260
PetPresetLoadButton.OnClick = function (sender)
 if PetPresetComboBox.ItemIndex == 0 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3'])
 elseif PetPresetComboBox.ItemIndex == 1 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-1'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-1'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-1'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-1'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-1'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-1'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-1'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-1'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-1'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-1'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-1'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-1'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-1'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-1'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-1'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-1'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-1'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-1'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-1'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-1'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-1'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-1'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-1'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-1'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-1'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-1'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-1'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-1'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-1'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-1'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-1'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-1'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-1'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-1'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-1'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-1'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-1'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-1'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-1'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-1'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-1'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-1'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-1'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-1'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-1'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-1'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-1'])
 elseif PetPresetComboBox.ItemIndex == 2 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-2'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-2'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-2'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-2'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-2'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-2'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-2'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-2'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-2'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-2'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-2'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-2'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-2'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-2'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-2'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-2'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-2'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-2'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-2'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-2'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-2'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-2'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-2'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-2'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-2'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-2'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-2'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-2'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-2'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-2'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-2'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-2'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-2'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-2'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-2'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-2'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-2'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-2'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-2'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-2'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-2'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-2'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-2'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-2'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-2'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-2'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-2'])
  elseif PetPresetComboBox.ItemIndex == 3 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-3'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-3'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-3'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-3'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-3'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-3'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-3'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-3'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-3'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-3'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-3'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-3'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-3'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-3'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-3'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-3'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-3'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-3'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-3'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-3'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-3'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-3'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-3'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-3'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-3'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-3'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-3'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-3'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-3'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-3'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-3'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-3'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-3'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-3'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-3'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-3'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-3'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-3'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-3'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-3'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-3'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-3'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-3'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-3'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-3'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-3'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-3'])
 elseif PresetComboBox.ItemIndex == 4 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-4'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-4'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-4'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-4'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-4'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-4'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-4'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-4'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-4'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-4'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-4'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-4'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-4'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-4'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-4'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-4'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-4'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-4'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-4'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-4'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-4'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-4'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-4'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-4'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-4'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-4'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-4'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-4'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-4'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-4'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-4'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-4'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-4'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-4'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-4'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-4'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-4'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-4'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-4'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-4'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-4'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-4'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-4'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-4'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-4'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-4'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-4'])
elseif PetPresetComboBox.ItemIndex == 5 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-5'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-5'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-5'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-5'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-5'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-5'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-5'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-5'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-5'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-5'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-5'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-5'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-5'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-5'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-5'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-5'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-5'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-5'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-5'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-5'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-5'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-5'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-5'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-5'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-5'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-5'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-5'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-5'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-5'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-5'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-5'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-5'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-5'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-5'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-5'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-5'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-5'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-5'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-5'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-5'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-5'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-5'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-5'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-5'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-5'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-5'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-5'])
elseif PetPresetComboBox.ItemIndex == 6 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-6'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-6'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-6'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-6'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-6'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-6'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-6'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-6'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-6'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-6'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-6'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-6'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-6'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-6'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-6'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-6'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-6'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-6'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-6'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-6'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-6'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-6'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-6'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-6'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-6'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-6'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-6'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-6'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-6'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-6'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-6'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-6'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-6'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-6'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-6'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-6'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-6'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-6'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-6'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-6'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-6'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-6'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-6'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-6'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-6'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-6'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-6'])
elseif PetPresetComboBox.ItemIndex == 7 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-7'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-7'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-7'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-7'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-7'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-7'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-7'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-7'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-7'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-7'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-7'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-7'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-7'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-7'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-7'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-7'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-7'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-7'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-7'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-7'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-7'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-7'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-7'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-7'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-7'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-7'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-7'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-7'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-7'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-7'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-7'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-7'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-7'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-7'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-7'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-7'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-7'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-7'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-7'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-7'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-7'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-7'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-7'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-7'])
 setProperty(PetsliderHB, 'Position', settings.Value['HBedit-7'])
 setProperty(PetsliderHB2, 'Position', settings.Value['HBedit2-7'])
 setProperty(PetsliderHB3, 'Position', settings.Value['HBedit3-7'])
elseif PetPresetComboBox.ItemIndex == 8 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-8'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-8'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-8'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-8'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-8'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-8'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-8'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-8'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-8'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-8'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-8'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-8'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-8'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-8'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-8'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-8'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-8'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-8'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-8'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-8'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-8'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-8'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-8'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-8'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-8'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-8'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-8'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-8'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-8'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-8'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-8'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-8'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-8'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-8'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-8'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-8'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-8'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-8'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-8'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-8'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-8'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-8'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-8'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-8'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-8'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-8'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-8'])
 elseif PetPresetComboBox.ItemIndex == 9 then
 setProperty(Petslider, 'Position', settings.Value['PetMainedit-9'])
 setProperty(Petslider2, 'Position', settings.Value['PetMainedit2-9'])
 setProperty(Petslider3, 'Position', settings.Value['PetMainedit3-9'])
 setProperty(Petslider4, 'Position', settings.Value['PetMainedit4-9'])
 setProperty(Petslider5, 'Position', settings.Value['PetMainedit5-9'])
 setProperty(Petslider6, 'Position', settings.Value['PetMainedit6-9'])
 setProperty(Petslider7, 'Position', settings.Value['PetMainedit7-9'])
 setProperty(Petslider8, 'Position', settings.Value['PetMainedit8-9'])
 setProperty(PetsliderBS, 'Position', settings.Value['PetBSedit-9'])
 setProperty(PetsliderBS2, 'Position', settings.Value['PetBSedit2-9'])
 setProperty(PetsliderBS3, 'Position', settings.Value['PetBSedit3-9'])
 setProperty(PetsliderBS4, 'Position', settings.Value['PetBSedit4-9'])
 setProperty(PetsliderBS5, 'Position', settings.Value['PetBSedit5-9'])
 setProperty(PetsliderBS6, 'Position', settings.Value['PetBSedit6-9'])
 setProperty(PetsliderBS7, 'Position', settings.Value['PetBSedit7-9'])
 setProperty(PetsliderBS8, 'Position', settings.Value['PetBSedit8-9'])
 setProperty(PetsliderBR2, 'Position', settings.Value['PetBRedit2-9'])
 setProperty(PetsliderBR3, 'Position', settings.Value['PetBRedit3-9'])
 setProperty(PetsliderBR4, 'Position', settings.Value['PetBRedit4-9'])
 setProperty(PetsliderBR5, 'Position', settings.Value['PetBRedit5-9'])
 setProperty(PetsliderBR6, 'Position', settings.Value['PetBRedit6-9'])
 setProperty(PetsliderBR7, 'Position', settings.Value['PetBRedit7-9'])
 setProperty(PetsliderBR8, 'Position', settings.Value['PetBRedit8-9'])
 setProperty(PetsliderBPX2, 'Position', settings.Value['PetBPeditX2-9'])
 setProperty(PetsliderBPX3, 'Position', settings.Value['PetBPeditX3-9'])
 setProperty(PetsliderBPX4, 'Position', settings.Value['PetBPeditX4-9'])
 setProperty(PetsliderBPX5, 'Position', settings.Value['PetBPeditX5-9'])
 setProperty(PetsliderBPX6, 'Position', settings.Value['PetBPeditX6-9'])
 setProperty(PetsliderBPX7, 'Position', settings.Value['PetBPeditX7-9'])
 setProperty(PetsliderBPX8, 'Position', settings.Value['PetBPeditX8-9'])
 setProperty(PetsliderBPY2, 'Position', settings.Value['PetBPeditY2-9'])
 setProperty(PetsliderBPY3, 'Position', settings.Value['PetBPeditY3-9'])
 setProperty(PetsliderBPY4, 'Position', settings.Value['PetBPeditY4-9'])
 setProperty(PetsliderBPY5, 'Position', settings.Value['PetBPeditY5-9'])
 setProperty(PetsliderBPY6, 'Position', settings.Value['PetBPeditY6-9'])
 setProperty(PetsliderBPY7, 'Position', settings.Value['PetBPeditY7-9'])
 setProperty(PetsliderBPY8, 'Position', settings.Value['PetBPeditY8-9'])
 setProperty(PetsliderBPZ2, 'Position', settings.Value['PetBPeditZ2-9'])
 setProperty(PetsliderBPZ3, 'Position', settings.Value['PetBPeditZ3-9'])
 setProperty(PetsliderBPZ4, 'Position', settings.Value['PetBPeditZ4-9'])
 setProperty(PetsliderBPZ5, 'Position', settings.Value['PetBPeditZ5-9'])
 setProperty(PetsliderBPZ6, 'Position', settings.Value['PetBPeditZ6-9'])
 setProperty(PetsliderBPZ7, 'Position', settings.Value['PetBPeditZ7-9'])
 setProperty(PetsliderBPZ8, 'Position', settings.Value['PetBPeditZ8-9'])
 setProperty(PetsliderHB, 'Position', settings.Value['PetHBedit-9'])
 setProperty(PetsliderHB2, 'Position', settings.Value['PetHBedit2-9'])
 setProperty(PetsliderHB3, 'Position', settings.Value['PetHBedit3-9'])
 end
end
Pettoggle=createToggleBox(PetModelForm)
checkbox_setState(Pettoggle, 1)
Pettoggle.Caption='Main'
Pettoggle.Left = 10
Pettoggle.OnChange = function (sender)
  if (checkbox_getState(Pettoggle) == 1) then
   checkbox_setState(PettoggleBS, 0)
   checkbox_setState(PettoggleBR, 0)
   checkbox_setState(PettoggleBP, 0)
   checkbox_setState(PettoggleHB, 0)
   Petslider.Visible = true
   Petslider2.Visible = true
   Petslider3.Visible = true
   Petslider4.Visible = true
   Petslider5.Visible = true
   Petslider6.Visible = true
   Petslider7.Visible = true
   Petslider8.Visible = true
   PetMainHair.Visible = true
   PetMainFace.Visible = true
   PetMainHands.Visible = true
   PetMainFeet.Visible = true
   PetMainChest.Visible = true
   PetMainShoul.Visible = true
   PetMainBack.Visible = true
   PetMainWings.Visible = true
   PetMainedit.Visible = true
   PetMainedit2.Visible = true
   PetMainedit3.Visible = true
   PetMainedit4.Visible = true
   PetMainedit5.Visible = true
   PetMainedit6.Visible = true
   PetMainedit7.Visible = true
   PetMainedit8.Visible = true
  elseif (checkbox_getState(Pettoggle) == 0) then
   Petslider.Visible = false
   Petslider2.Visible = false
   Petslider3.Visible = false
   Petslider4.Visible = false
   Petslider5.Visible = false
   Petslider6.Visible = false
   Petslider7.Visible = false
   Petslider8.Visible = false
   PetMainHair.Visible = false
   PetMainFace.Visible = false
   PetMainHands.Visible = false
   PetMainFeet.Visible = false
   PetMainChest.Visible = false
   PetMainShoul.Visible = false
   PetMainBack.Visible = false
   PetMainWings.Visible = false
   PetMainedit.Visible = false
   PetMainedit2.Visible = false
   PetMainedit3.Visible = false
   PetMainedit4.Visible = false
   PetMainedit5.Visible = false
   PetMainedit6.Visible = false
   PetMainedit7.Visible = false
   PetMainedit8.Visible = false
  end
end
PettoggleBS=createToggleBox(PetModelForm)
PettoggleBS.Caption='BodySizes'
PettoggleBS.Left = 85
PettoggleBS.OnClick = function (sender)
  if(checkbox_getState(PettoggleBS) == 1) then
   checkbox_setState(Pettoggle, 0)
   checkbox_setState(PettoggleBR, 0)
   checkbox_setState(PettoggleBP, 0)
   checkbox_setState(PettoggleHB, 0)
   PetsliderBS.Visible = true
   PetsliderBS2.Visible = true
   PetsliderBS3.Visible = true
   PetsliderBS4.Visible = true
   PetsliderBS5.Visible = true
   PetsliderBS6.Visible = true
   PetsliderBS7.Visible = true
   PetsliderBS8.Visible = true
   PetSizeHead.Visible = true
   PetSizeChest.Visible = true
   PetSizeHands.Visible = true
   PetSizeFeet.Visible = true
   PetSizeShoul.Visible = true
   PetSizeBack.Visible = true
   PetSizeWings.Visible = true
   PetSizeWeap.Visible = true
   PetBSedit.Visible = true
   PetBSedit2.Visible = true
   PetBSedit3.Visible = true
   PetBSedit4.Visible = true
   PetBSedit5.Visible = true
   PetBSedit6.Visible = true
   PetBSedit7.Visible = true
   PetBSedit8.Visible = true
  elseif (checkbox_getState(PettoggleBS) == 0) then
   PetsliderBS.Visible = false
   PetsliderBS2.Visible = false
   PetsliderBS3.Visible = false
   PetsliderBS4.Visible = false
   PetsliderBS5.Visible = false
   PetsliderBS6.Visible = false
   PetsliderBS7.Visible = false
   PetsliderBS8.Visible = false
   PetSizeHead.Visible = false
   PetSizeChest.Visible = false
   PetSizeHands.Visible = false
   PetSizeFeet.Visible = false
   PetSizeShoul.Visible = false
   PetSizeBack.Visible = false
   PetSizeWings.Visible = false
   PetSizeWeap.Visible = false
   PetBSedit.Visible = false
   PetBSedit2.Visible = false
   PetBSedit3.Visible = false
   PetBSedit4.Visible = false
   PetBSedit5.Visible = false
   PetBSedit6.Visible = false
   PetBSedit7.Visible = false
   PetBSedit8.Visible = false
  end
end
PettoggleBR=createToggleBox(PetModelForm)
PettoggleBR.Caption='Rotations'
PettoggleBR.Left = 160
PettoggleBR.OnClick = function (sender)
  if(checkbox_getState(PettoggleBR) == 1) then
   checkbox_setState(Pettoggle, 0)
   checkbox_setState(PettoggleBS, 0)
   checkbox_setState(PettoggleBP, 0)
   checkbox_setState(PettoggleHB, 0)
   PetsliderBR2.Visible = true
   PetsliderBR3.Visible = true
   PetsliderBR4.Visible = true
   PetsliderBR5.Visible = true
   PetsliderBR6.Visible = true
   PetsliderBR7.Visible = true
   PetsliderBR8.Visible = true
   PetRotationChestZY.Visible = true
   PetRotationHandsZY.Visible = true
   PetRotationHandsXY.Visible = true
   PetRotationHandsZX.Visible = true
   PetRotationFeetZY.Visible = true
   PetRotationWingsZY.Visible = true
   PetRotationBackZY.Visible = true
   PetBRedit2.Visible = true
   PetBRedit3.Visible = true
   PetBRedit4.Visible = true
   PetBRedit5.Visible = true
   PetBRedit6.Visible = true
   PetBRedit7.Visible = true
   PetBRedit8.Visible = true
  elseif (checkbox_getState(PettoggleBR) == 0) then
   PetsliderBR2.Visible = false
   PetsliderBR3.Visible = false
   PetsliderBR4.Visible = false
   PetsliderBR5.Visible = false
   PetsliderBR6.Visible = false
   PetsliderBR7.Visible = false
   PetsliderBR8.Visible = false
   PetRotationChestZY.Visible = false
   PetRotationHandsZY.Visible = false
   PetRotationHandsXY.Visible = false
   PetRotationHandsZX.Visible = false
   PetRotationFeetZY.Visible = false
   PetRotationWingsZY.Visible = false
   PetRotationBackZY.Visible = false
   PetBRedit2.Visible = false
   PetBRedit3.Visible = false
   PetBRedit4.Visible = false
   PetBRedit5.Visible = false
   PetBRedit6.Visible = false
   PetBRedit7.Visible = false
   PetBRedit8.Visible = false
  end
end
PettoggleBP=createToggleBox(PetModelForm)
PettoggleBP.Caption='Positions'
PettoggleBP.Left = 235
PettoggleBP.OnClick = function (sender)
  if(checkbox_getState(PettoggleBP) == 1) then
   checkbox_setState(Pettoggle, 0)
   checkbox_setState(PettoggleBS, 0)
   checkbox_setState(PettoggleBR, 0)
   checkbox_setState(PettoggleHB, 0)
   PetsliderBPX.Visible = true
   PetsliderBPX2.Visible = true
   PetsliderBPX3.Visible = true
   PetsliderBPX4.Visible = true
   PetsliderBPX5.Visible = true
   PetsliderBPX6.Visible = true
   PetsliderBPY1.Visible = true
   PetsliderBPY2.Visible = true
   PetsliderBPY3.Visible = true
   PetsliderBPY4.Visible = true
   PetsliderBPY5.Visible = true
   PetsliderBPY6.Visible = true
   PetsliderBPZ1.Visible = true
   PetsliderBPZ2.Visible = true
   PetsliderBPZ3.Visible = true
   PetsliderBPZ4.Visible = true
   PetsliderBPZ5.Visible = true
   PetsliderBPZ6.Visible = true
   PetPositionCentralBody.Visible = true
   PetPositionHead.Visible = true
   PetPositionHands.Visible = true
   PetPositionFeet.Visible = true
   PetPositionWings.Visible = true
   PetPositionBack.Visible = true
   PetPositionCentralBodyx.Visible = true
   PetPositionHeadx.Visible = true
   PetPositionHandsx.Visible = true
   PetPositionFeetx.Visible = true
   PetPositionWingsx.Visible = true
   PetPositionBackx.Visible = true
   PetPositionCentralBodyy.Visible = true
   PetPositionHeady.Visible = true
   PetPositionHandsy.Visible = true
   PetPositionFeety.Visible = true
   PetPositionWingsy.Visible = true
   PetPositionBacky.Visible = true
   PetPositionCentralBodyz.Visible = true
   PetPositionHeadz.Visible = true
   PetPositionHandsz.Visible = true
   PetPositionFeetz.Visible = true
   PetPositionWingsz.Visible = true
   PetPositionBackz.Visible = true
   PetBPeditX2.Visible = true
   PetBPeditX3.Visible = true
   PetBPeditX4.Visible = true
   PetBPeditX5.Visible = true
   PetBPeditX6.Visible = true
   PetBPeditX7.Visible = true
   PetBPeditY2.Visible = true
   PetBPeditY3.Visible = true
   PetBPeditY4.Visible = true
   PetBPeditY5.Visible = true
   PetBPeditY6.Visible = true
   PetBPeditY7.Visible = true
   PetBPeditZ2.Visible = true
   PetBPeditZ3.Visible = true
   PetBPeditZ4.Visible = true
   PetBPeditZ5.Visible = true
   PetBPeditZ6.Visible = true
   PetBPeditZ7.Visible = true
  elseif (checkbox_getState(PettoggleBP) == 0) then
  PetsliderBPX.Visible = false
  PetsliderBPX2.Visible = false
  PetsliderBPX3.Visible = false
  PetsliderBPX4.Visible = false
  PetsliderBPX5.Visible = false
  PetsliderBPX6.Visible = false
  PetsliderBPY1.Visible = false
  PetsliderBPY2.Visible = false
  PetsliderBPY3.Visible = false
  PetsliderBPY4.Visible = false
  PetsliderBPY5.Visible = false
  PetsliderBPY6.Visible = false
  PetsliderBPZ1.Visible = false
  PetsliderBPZ2.Visible = false
  PetsliderBPZ3.Visible = false
  PetsliderBPZ4.Visible = false
  PetsliderBPZ5.Visible = false
  PetsliderBPZ6.Visible = false
  PetPositionCentralBody.Visible = false
  PetPositionHead.Visible = false
  PetPositionHands.Visible = false
  PetPositionFeet.Visible = false
  PetPositionWings.Visible = false
  PetPositionBack.Visible = false
  PetPositionCentralBodyx.Visible = false
  PetPositionHeadx.Visible = false
  PetPositionHandsx.Visible = false
  PetPositionFeetx.Visible = false
  PetPositionWingsx.Visible = false
  PetPositionBackx.Visible = false
  PetPositionCentralBodyy.Visible = false
  PetPositionHeady.Visible = false
  PetPositionHandsy.Visible = false
  PetPositionFeety.Visible = false
  PetPositionWingsy.Visible = false
  PetPositionBacky.Visible = false
  PetPositionCentralBodyz.Visible = false
  PetPositionHeadz.Visible = false
  PetPositionHandsz.Visible = false
  PetPositionFeetz.Visible = false
  PetPositionWingsz.Visible = false
  PetPositionBackz.Visible = false
  PetBPeditX2.Visible = false
  PetBPeditX3.Visible = false
  PetBPeditX4.Visible = false
  PetBPeditX5.Visible = false
  PetBPeditX6.Visible = false
  PetBPeditX7.Visible = false
  PetBPeditY2.Visible = false
  PetBPeditY3.Visible = false
  PetBPeditY4.Visible = false
  PetBPeditY5.Visible = false
  PetBPeditY6.Visible = false
  PetBPeditY7.Visible = false
  PetBPeditZ2.Visible = false
  PetBPeditZ3.Visible = false
  PetBPeditZ4.Visible = false
  PetBPeditZ5.Visible = false
  PetBPeditZ6.Visible = false
  PetBPeditZ7.Visible = false
  end
end
PettoggleHB=createToggleBox(PetModelForm)
PettoggleHB.Caption='Hitbox'
PettoggleHB.Left = 310
PettoggleHB.OnClick = function (sender)
  if(checkbox_getState(PettoggleHB) == 1) then
   checkbox_setState(Pettoggle, 0)
   checkbox_setState(PettoggleBS, 0)
   checkbox_setState(PettoggleBP, 0)
   checkbox_setState(PettoggleBR, 0)
   PetsliderHB.Visible = true
   PetsliderHB2.Visible = true
   PetsliderHB3.Visible = true
   PetHBHeight.Visible = true
   PetHBScaleHeight.Visible = true
   PetHBScaleWidth.Visible = true
   PetHBedit.Visible = true
   PetHBedit2.Visible = true
   PetHBedit3.Visible = true
  elseif (checkbox_getState(PettoggleHB) == 0) then
   PetsliderHB.Visible = false
   PetsliderHB2.Visible = false
   PetsliderHB3.Visible = false
   PetHBHeight.Visible = false
   PetHBScaleHeight.Visible = false
   PetHBScaleWidth.Visible = false
   PetHBedit.Visible = false
   PetHBedit2.Visible = false
   PetHBedit3.Visible = false
  end
end
Petslider=createTrackBar(PetModelForm)
Petslider.Width = 300
Petslider.Height = 25
Petslider.Left = 50
Petslider.Top = 50
Petslider.Max = 3652
Petslider.Min = 0
Petslider2=createTrackBar(PetModelForm)
Petslider2.Width = 300
Petslider2.Height = 25
Petslider2.Left = 50
Petslider2.Top = 100
Petslider2.Max = 3652
Petslider2.Min = 0
Petslider3=createTrackBar(PetModelForm)
Petslider3.Width = 300
Petslider3.Height = 25
Petslider3.Left = 50
Petslider3.Top = 150
Petslider3.Max = 3652
Petslider3.Min = 0
Petslider4=createTrackBar(PetModelForm)
Petslider4.Width = 300
Petslider4.Height = 25
Petslider4.Left = 50
Petslider4.Top = 200
Petslider4.Max = 3652
Petslider4.Min = 0
Petslider5=createTrackBar(PetModelForm)
Petslider5.Width = 300
Petslider5.Height = 25
Petslider5.Left = 50
Petslider5.Top = 250
Petslider5.Max = 3652
Petslider5.Min = 0
Petslider6=createTrackBar(PetModelForm)
Petslider6.Width = 300
Petslider6.Height = 25
Petslider6.Left = 50
Petslider6.Top = 300
Petslider6.Max = 3652
Petslider6.Min = 0
Petslider7=createTrackBar(PetModelForm)
Petslider7.Width = 300
Petslider7.Height = 25
Petslider7.Left = 50
Petslider7.Top = 350
Petslider7.Max = 3652
Petslider7.Min = 0
Petslider8=createTrackBar(PetModelForm)
Petslider8.Width = 300
Petslider8.Height = 25
Petslider8.Left = 50
Petslider8.Top = 400
Petslider8.Max = 3652
Petslider8.Min = 0
PetsliderBR2=createTrackBar(PetModelForm)
PetsliderBR2.Width = 300
PetsliderBR2.Height = 25
PetsliderBR2.Left = 50
PetsliderBR2.Top = 100
PetsliderBR2.Max = 180
PetsliderBR2.Min = -180
PetsliderBR3=createTrackBar(PetModelForm)
PetsliderBR3.Width = 300
PetsliderBR3.Height = 25
PetsliderBR3.Left = 50
PetsliderBR3.Top = 150
PetsliderBR3.Max = 180
PetsliderBR3.Min = -180
PetsliderBR4=createTrackBar(PetModelForm)
PetsliderBR4.Width = 300
PetsliderBR4.Height = 25
PetsliderBR4.Left = 50
PetsliderBR4.Top = 200
PetsliderBR4.Max = 180
PetsliderBR4.Min = -180
PetsliderBR5=createTrackBar(PetModelForm)
PetsliderBR5.Width = 300
PetsliderBR5.Height = 25
PetsliderBR5.Left = 50
PetsliderBR5.Top = 250
PetsliderBR5.Max = 180
PetsliderBR5.Min = -180
PetsliderBR6=createTrackBar(PetModelForm)
PetsliderBR6.Width = 300
PetsliderBR6.Height = 25
PetsliderBR6.Left = 50
PetsliderBR6.Top = 300
PetsliderBR6.Max = 180
PetsliderBR6.Min = -180
PetsliderBR7=createTrackBar(PetModelForm)
PetsliderBR7.Width = 300
PetsliderBR7.Height = 25
PetsliderBR7.Left = 50
PetsliderBR7.Top = 350
PetsliderBR7.Max = 180
PetsliderBR7.Min = -180
PetsliderBR8=createTrackBar(PetModelForm)
PetsliderBR8.Width = 300
PetsliderBR8.Height = 25
PetsliderBR8.Left = 50
PetsliderBR8.Top = 400
PetsliderBR8.Max = 180
PetsliderBR8.Min = -180
PetsliderBR2.Visible = false
PetsliderBR3.Visible = false
PetsliderBR4.Visible = false
PetsliderBR5.Visible = false
PetsliderBR6.Visible = false
PetsliderBR7.Visible = false
PetsliderBR8.Visible = false
PetsliderBS=createTrackBar(PetModelForm)
PetsliderBS.Width = 300
PetsliderBS.Height = 25
PetsliderBS.Left = 50
PetsliderBS.Top = 50
PetsliderBS.Max = 250
PetsliderBS.Min = 0
PetsliderBS2=createTrackBar(PetModelForm)
PetsliderBS2.Width = 300
PetsliderBS2.Height = 25
PetsliderBS2.Left = 50
PetsliderBS2.Top = 100
PetsliderBS2.Max = 250
PetsliderBS2.Min = 0
PetsliderBS3=createTrackBar(PetModelForm)
PetsliderBS3.Width = 300
PetsliderBS3.Height = 25
PetsliderBS3.Left = 50
PetsliderBS3.Top = 150
PetsliderBS3.Max = 250
PetsliderBS3.Min = 0
PetsliderBS4=createTrackBar(PetModelForm)
PetsliderBS4.Width = 300
PetsliderBS4.Height = 25
PetsliderBS4.Left = 50
PetsliderBS4.Top = 200
PetsliderBS4.Max = 250
PetsliderBS4.Min = 0
PetsliderBS5=createTrackBar(PetModelForm)
PetsliderBS5.Width = 300
PetsliderBS5.Height = 25
PetsliderBS5.Left = 50
PetsliderBS5.Top = 250
PetsliderBS5.Max = 250
PetsliderBS5.Min = 0
PetsliderBS6=createTrackBar(PetModelForm)
PetsliderBS6.Width = 300
PetsliderBS6.Height = 25
PetsliderBS6.Left = 50
PetsliderBS6.Top = 300
PetsliderBS6.Max = 250
PetsliderBS6.Min = 0
PetsliderBS7=createTrackBar(PetModelForm)
PetsliderBS7.Width = 300
PetsliderBS7.Height = 25
PetsliderBS7.Left = 50
PetsliderBS7.Top = 350
PetsliderBS7.Max = 250
PetsliderBS7.Min = 0
PetsliderBS8=createTrackBar(PetModelForm)
PetsliderBS8.Width = 300
PetsliderBS8.Height = 25
PetsliderBS8.Left = 50
PetsliderBS8.Top = 400
PetsliderBS8.Max = 250
PetsliderBS8.Min = 0
PetsliderBS.Visible = false
PetsliderBS2.Visible = false
PetsliderBS3.Visible = false
PetsliderBS4.Visible = false
PetsliderBS5.Visible = false
PetsliderBS6.Visible = false
PetsliderBS7.Visible = false
PetsliderBS8.Visible = false
PetsliderBPX=createTrackBar(PetModelForm)
PetsliderBPX.Width = 125
PetsliderBPX.Height = 25
PetsliderBPX.Left = 10
PetsliderBPX.Top = 70
PetsliderBPX.Max = 100
PetsliderBPX.Min = -100
PetsliderBPX2=createTrackBar(PetModelForm)
PetsliderBPX2.Width = 125
PetsliderBPX2.Height = 25
PetsliderBPX2.Left = 10
PetsliderBPX2.Top = 140
PetsliderBPX2.Max = 100
PetsliderBPX2.Min = -100
PetsliderBPX3=createTrackBar(PetModelForm)
PetsliderBPX3.Width = 125
PetsliderBPX3.Height = 25
PetsliderBPX3.Left = 10
PetsliderBPX3.Top = 210
PetsliderBPX3.Max = 100
PetsliderBPX3.Min = -100
PetsliderBPX4=createTrackBar(PetModelForm)
PetsliderBPX4.Width = 125
PetsliderBPX4.Height = 25
PetsliderBPX4.Left = 10
PetsliderBPX4.Top = 280
PetsliderBPX4.Max = 100
PetsliderBPX4.Min = -100
PetsliderBPX5=createTrackBar(PetModelForm)
PetsliderBPX5.Width = 125
PetsliderBPX5.Height = 25
PetsliderBPX5.Left = 10
PetsliderBPX5.Top = 350
PetsliderBPX5.Max = 100
PetsliderBPX5.Min = -100
PetsliderBPX6=createTrackBar(PetModelForm)
PetsliderBPX6.Width = 125
PetsliderBPX6.Height = 25
PetsliderBPX6.Left = 10
PetsliderBPX6.Top = 420
PetsliderBPX6.Max = 100
PetsliderBPX6.Min = -100
PetsliderBPY1=createTrackBar(PetModelForm)
PetsliderBPY1.Width = 125
PetsliderBPY1.Height = 25
PetsliderBPY1.Left = 140
PetsliderBPY1.Top = 70
PetsliderBPY1.Max = 100
PetsliderBPY1.Min = -100
PetsliderBPY2=createTrackBar(PetModelForm)
PetsliderBPY2.Width = 125
PetsliderBPY2.Height = 25
PetsliderBPY2.Left = 140
PetsliderBPY2.Top = 140
PetsliderBPY2.Max = 100
PetsliderBPY2.Min = -100
PetsliderBPY3=createTrackBar(PetModelForm)
PetsliderBPY3.Width = 125
PetsliderBPY3.Height = 25
PetsliderBPY3.Left = 140
PetsliderBPY3.Top = 210
PetsliderBPY3.Max = 100
PetsliderBPY3.Min = -100
PetsliderBPY4=createTrackBar(PetModelForm)
PetsliderBPY4.Width = 125
PetsliderBPY4.Height = 25
PetsliderBPY4.Left = 140
PetsliderBPY4.Top = 280
PetsliderBPY4.Max = 100
PetsliderBPY4.Min = -100
PetsliderBPY5=createTrackBar(PetModelForm)
PetsliderBPY5.Width = 125
PetsliderBPY5.Height = 25
PetsliderBPY5.Left = 140
PetsliderBPY5.Top = 350
PetsliderBPY5.Max = 100
PetsliderBPY5.Min = -100
PetsliderBPY6=createTrackBar(PetModelForm)
PetsliderBPY6.Width = 125
PetsliderBPY6.Height = 25
PetsliderBPY6.Left = 140
PetsliderBPY6.Top = 420
PetsliderBPY6.Max = 100
PetsliderBPY6.Min = -100
PetsliderBPZ1=createTrackBar(PetModelForm)
PetsliderBPZ1.Width = 125
PetsliderBPZ1.Height = 25
PetsliderBPZ1.Left = 270
PetsliderBPZ1.Top = 70
PetsliderBPZ1.Max = 100
PetsliderBPZ1.Min = -100
PetsliderBPZ2=createTrackBar(PetModelForm)
PetsliderBPZ2.Width = 125
PetsliderBPZ2.Height = 25
PetsliderBPZ2.Left = 270
PetsliderBPZ2.Top = 140
PetsliderBPZ2.Max = 100
PetsliderBPZ2.Min = -100
PetsliderBPZ3=createTrackBar(PetModelForm)
PetsliderBPZ3.Width = 125
PetsliderBPZ3.Height = 25
PetsliderBPZ3.Left = 270
PetsliderBPZ3.Top = 210
PetsliderBPZ3.Max = 100
PetsliderBPZ3.Min = -100
PetsliderBPZ4=createTrackBar(PetModelForm)
PetsliderBPZ4.Width = 125
PetsliderBPZ4.Height = 25
PetsliderBPZ4.Left = 270
PetsliderBPZ4.Top = 280
PetsliderBPZ4.Max = 100
PetsliderBPZ4.Min = -100
PetsliderBPZ5=createTrackBar(PetModelForm)
PetsliderBPZ5.Width = 125
PetsliderBPZ5.Height = 25
PetsliderBPZ5.Left = 270
PetsliderBPZ5.Top = 350
PetsliderBPZ5.Max = 100
PetsliderBPZ5.Min = -100
PetsliderBPZ6=createTrackBar(PetModelForm)
PetsliderBPZ6.Width = 125
PetsliderBPZ6.Height = 25
PetsliderBPZ6.Left = 270
PetsliderBPZ6.Top = 420
PetsliderBPZ6.Max = 100
PetsliderBPZ6.Min = -100
PetsliderBPX.Visible = false
PetsliderBPX2.Visible = false
PetsliderBPX3.Visible = false
PetsliderBPX4.Visible = false
PetsliderBPX5.Visible = false
PetsliderBPX6.Visible = false
PetsliderBPY1.Visible = false
PetsliderBPY2.Visible = false
PetsliderBPY3.Visible = false
PetsliderBPY4.Visible = false
PetsliderBPY5.Visible = false
PetsliderBPY6.Visible = false
PetsliderBPZ1.Visible = false
PetsliderBPZ2.Visible = false
PetsliderBPZ3.Visible = false
PetsliderBPZ4.Visible = false
PetsliderBPZ5.Visible = false
PetsliderBPZ6.Visible = false
PetsliderHB=createTrackBar(PetModelForm)
PetsliderHB.Width = 300
PetsliderHB.Height = 25
PetsliderHB.Left = 50
PetsliderHB.Top = 150
PetsliderHB.Max = 1000
PetsliderHB.Min = 0
PetsliderHB2=createTrackBar(PetModelForm)
PetsliderHB2.Width = 300
PetsliderHB2.Height = 25
PetsliderHB2.Left = 50
PetsliderHB2.Top = 250
PetsliderHB2.Max = 250
PetsliderHB2.Min = 0
PetsliderHB3=createTrackBar(PetModelForm)
PetsliderHB3.Width = 300
PetsliderHB3.Height = 25
PetsliderHB3.Left = 50
PetsliderHB3.Top = 350
PetsliderHB3.Max = 250
PetsliderHB3.Min = 0
PetsliderHB.Visible = false
PetsliderHB2.Visible = false
PetsliderHB3.Visible = false
PetMainHair=createLabel(PetModelForm)
PetMainHair.setCaption('Hair:')
PetMainHair.Font.Color = 0xffffff
PetMainHair.Font.Size = 14
PetMainHair.Font.Style = ('fsUnderline, fsBold')
PetMainHair.Top = 45
PetMainHair.Left = 5
PetMainFace=createLabel(PetModelForm)
PetMainFace.setCaption('Face:')
PetMainFace.Font.Color = 0xffffff
PetMainFace.Font.Size = 14
PetMainFace.Font.Style = ('fsUnderline, fsBold')
PetMainFace.Top = 95
PetMainFace.Left = 5
PetMainHands=createLabel(PetModelForm)
PetMainHands.setCaption('Hands:')
PetMainHands.Font.Color = 0xffffff
PetMainHands.Font.Size = 12
PetMainHands.Font.Style = ('fsUnderline, fsBold')
PetMainHands.Top = 145
PetMainHands.Left = 5
PetMainFeet=createLabel(PetModelForm)
PetMainFeet.setCaption('Feet:')
PetMainFeet.Font.Color = 0xffffff
PetMainFeet.Font.Size = 14
PetMainFeet.Font.Style = ('fsUnderline, fsBold')
PetMainFeet.Top = 195
PetMainFeet.Left = 5
PetMainChest=createLabel(PetModelForm)
PetMainChest.setCaption('Chest:')
PetMainChest.Font.Color = 0xffffff
PetMainChest.Font.Size = 14
PetMainChest.Font.Style = ('fsUnderline, fsBold')
PetMainChest.Top = 245
PetMainChest.Left = 5
PetMainShoul=createLabel(PetModelForm)
PetMainShoul.setCaption('Shoul.:')
PetMainShoul.Font.Color = 0xffffff
PetMainShoul.Font.Size = 12
PetMainShoul.Font.Style = ('fsUnderline, fsBold')
PetMainShoul.Top = 295
PetMainShoul.Left = 5
PetMainBack=createLabel(PetModelForm)
PetMainBack.setCaption('Back:')
PetMainBack.Font.Color = 0xffffff
PetMainBack.Font.Size = 14
PetMainBack.Font.Style = ('fsUnderline, fsBold')
PetMainBack.Top = 345
PetMainBack.Left = 5
PetMainWings=createLabel(PetModelForm)
PetMainWings.setCaption('Wings:')
PetMainWings.Font.Color = 0xffffff
PetMainWings.Font.Size = 12
PetMainWings.Font.Style = ('fsUnderline, fsBold')
PetMainWings.Top = 395
PetMainWings.Left = 5
PetSizeHead=createLabel(PetModelForm)
PetSizeHead.setCaption('Head:')
PetSizeHead.Font.Color = 0xffffff
PetSizeHead.Font.Size = 14
PetSizeHead.Font.Style = ('fsUnderline, fsBold')
PetSizeHead.Top = 45
PetSizeHead.Left = 5
PetSizeChest=createLabel(PetModelForm)
PetSizeChest.setCaption('Chest:')
PetSizeChest.Font.Color = 0xffffff
PetSizeChest.Font.Size = 14
PetSizeChest.Font.Style = ('fsUnderline, fsBold')
PetSizeChest.Top = 95
PetSizeChest.Left = 5
PetSizeHands=createLabel(PetModelForm)
PetSizeHands.setCaption('Hands:')
PetSizeHands.Font.Color = 0xffffff
PetSizeHands.Font.Size = 12
PetSizeHands.Font.Style = ('fsUnderline, fsBold')
PetSizeHands.Top = 145
PetSizeHands.Left = 5
PetSizeFeet=createLabel(PetModelForm)
PetSizeFeet.setCaption('Feet:')
PetSizeFeet.Font.Color = 0xffffff
PetSizeFeet.Font.Size = 14
PetSizeFeet.Font.Style = ('fsUnderline, fsBold')
PetSizeFeet.Top = 195
PetSizeFeet.Left = 5
PetSizeShoul=createLabel(PetModelForm)
PetSizeShoul.setCaption('Shoul.:')
PetSizeShoul.Font.Color = 0xffffff
PetSizeShoul.Font.Size = 12
PetSizeShoul.Font.Style = ('fsUnderline, fsBold')
PetSizeShoul.Top = 245
PetSizeShoul.Left = 5
PetSizeBack=createLabel(PetModelForm)
PetSizeBack.setCaption('Back:')
PetSizeBack.Font.Color = 0xffffff
PetSizeBack.Font.Size = 14
PetSizeBack.Font.Style = ('fsUnderline, fsBold')
PetSizeBack.Top = 295
PetSizeBack.Left = 5
PetSizeWings=createLabel(PetModelForm)
PetSizeWings.setCaption('Wings:')
PetSizeWings.Font.Color = 0xffffff
PetSizeWings.Font.Size = 12
PetSizeWings.Font.Style = ('fsUnderline, fsBold')
PetSizeWings.Top = 345
PetSizeWings.Left = 5
PetSizeWeap=createLabel(PetModelForm)
PetSizeWeap.setCaption('Weap.:')
PetSizeWeap.Font.Color = 0xffffff
PetSizeWeap.Font.Size = 12
PetSizeWeap.Font.Style = ('fsUnderline, fsBold')
PetSizeWeap.Top = 395
PetSizeWeap.Left = 5
PetSizeHead.Visible = false
PetSizeChest.Visible = false
PetSizeHands.Visible = false
PetSizeFeet.Visible = false
PetSizeShoul.Visible = false
PetSizeBack.Visible = false
PetSizeWings.Visible = false
PetSizeWeap.Visible = false
PetRotationChestZY=createLabel(PetModelForm)
PetRotationChestZY.setCaption('ChestZY:')
PetRotationChestZY.Font.Color = 0xffffff
PetRotationChestZY.Font.Size = 10
PetRotationChestZY.Font.Style = ('fsUnderline, fsBold')
PetRotationChestZY.Top = 100
PetRotationChestZY.Left = 4
PetRotationHandsZY=createLabel(PetModelForm)
PetRotationHandsZY.setCaption('HandZY:')
PetRotationHandsZY.Font.Color = 0xffffff
PetRotationHandsZY.Font.Size = 10
PetRotationHandsZY.Font.Style = ('fsUnderline, fsBold')
PetRotationHandsZY.Top = 150
PetRotationHandsZY.Left = 4
PetRotationHandsXY=createLabel(PetModelForm)
PetRotationHandsXY.setCaption('HandXY:')
PetRotationHandsXY.Font.Color = 0xffffff
PetRotationHandsXY.Font.Size = 10
PetRotationHandsXY.Font.Style = ('fsUnderline, fsBold')
PetRotationHandsXY.Top = 200
PetRotationHandsXY.Left = 4
PetRotationHandsZX=createLabel(PetModelForm)
PetRotationHandsZX.setCaption('HandZX:')
PetRotationHandsZX.Font.Color = 0xffffff
PetRotationHandsZX.Font.Size = 10
PetRotationHandsZX.Font.Style = ('fsUnderline, fsBold')
PetRotationHandsZX.Top = 250
PetRotationHandsZX.Left = 4
PetRotationFeetZY=createLabel(PetModelForm)
PetRotationFeetZY.setCaption('FeetZY:')
PetRotationFeetZY.Font.Color = 0xffffff
PetRotationFeetZY.Font.Size = 10
PetRotationFeetZY.Font.Style = ('fsUnderline, fsBold')
PetRotationFeetZY.Top = 300
PetRotationFeetZY.Left = 5
PetRotationWingsZY=createLabel(PetModelForm)
PetRotationWingsZY.setCaption('WingZY:')
PetRotationWingsZY.Font.Color = 0xffffff
PetRotationWingsZY.Font.Size = 10
PetRotationWingsZY.Font.Style = ('fsUnderline, fsBold')
PetRotationWingsZY.Top = 350
PetRotationWingsZY.Left = 4
PetRotationBackZY=createLabel(PetModelForm)
PetRotationBackZY.setCaption('BackZY:')
PetRotationBackZY.Font.Color = 0xffffff
PetRotationBackZY.Font.Size = 10
PetRotationBackZY.Font.Style = ('fsUnderline, fsBold')
PetRotationBackZY.Top = 400
PetRotationBackZY.Left = 5
PetRotationChestZY.Visible = false
PetRotationHandsZY.Visible = false
PetRotationHandsXY.Visible = false
PetRotationHandsZX.Visible = false
PetRotationFeetZY.Visible = false
PetRotationWingsZY.Visible = false
PetRotationBackZY.Visible = false
PetPositionCentralBody=createLabel(PetModelForm)
PetPositionCentralBody.setCaption('CentralBody:')
PetPositionCentralBody.Font.Color = 0xffffff
PetPositionCentralBody.Font.Size = 12
PetPositionCentralBody.Font.Style = ('fsUnderline, fsBold')
PetPositionCentralBody.Top = 30
PetPositionCentralBody.Left = 152
PetPositionHead=createLabel(PetModelForm)
PetPositionHead.setCaption('Head:')
PetPositionHead.Font.Color = 0xffffff
PetPositionHead.Font.Size = 12
PetPositionHead.Font.Style = ('fsUnderline, fsBold')
PetPositionHead.Top = 100
PetPositionHead.Left = 181
PetPositionHands=createLabel(PetModelForm)
PetPositionHands.setCaption('Hands:')
PetPositionHands.Font.Color = 0xffffff
PetPositionHands.Font.Size = 12
PetPositionHands.Font.Style = ('fsUnderline, fsBold')
PetPositionHands.Top = 170
PetPositionHands.Left = 177
PetPositionFeet=createLabel(PetModelForm)
PetPositionFeet.setCaption('Feet:')
PetPositionFeet.Font.Color = 0xffffff
PetPositionFeet.Font.Size = 12
PetPositionFeet.Font.Style = ('fsUnderline, fsBold')
PetPositionFeet.Top = 240
PetPositionFeet.Left = 185
PetPositionWings=createLabel(PetModelForm)
PetPositionWings.setCaption('Wings:')
PetPositionWings.Font.Color = 0xffffff
PetPositionWings.Font.Size = 12
PetPositionWings.Font.Style = ('fsUnderline, fsBold')
PetPositionWings.Top = 310
PetPositionWings.Left = 177
PetPositionBack=createLabel(PetModelForm)
PetPositionBack.setCaption('Back:')
PetPositionBack.Font.Color = 0xffffff
PetPositionBack.Font.Size = 12
PetPositionBack.Font.Style = ('fsUnderline, fsBold')
PetPositionBack.Top = 380
PetPositionBack.Left = 182
PetPositionCentralBody.Visible = false
PetPositionHead.Visible = false
PetPositionHands.Visible = false
PetPositionFeet.Visible = false
PetPositionWings.Visible = false
PetPositionBack.Visible = false
PetPositionCentralBodyx=createLabel(PetModelForm)
PetPositionCentralBodyx.setCaption('X:')
PetPositionCentralBodyx.Font.Color = 0xffffff
PetPositionCentralBodyx.Font.Size = 8
PetPositionCentralBodyx.Font.Style = ('fsBold')
PetPositionCentralBodyx.Top = 75
PetPositionCentralBodyx.Left = 5
PetPositionHeadx=createLabel(PetModelForm)
PetPositionHeadx.setCaption('X:')
PetPositionHeadx.Font.Color = 0xffffff
PetPositionHeadx.Font.Size = 8
PetPositionHeadx.Font.Style = ('fsBold')
PetPositionHeadx.Top = 145
PetPositionHeadx.Left = 5
PetPositionHandsx=createLabel(PetModelForm)
PetPositionHandsx.setCaption('X:')
PetPositionHandsx.Font.Color = 0xffffff
PetPositionHandsx.Font.Size = 8
PetPositionHandsx.Font.Style = ('fsBold')
PetPositionHandsx.Top = 215
PetPositionHandsx.Left = 5
PetPositionFeetx=createLabel(PetModelForm)
PetPositionFeetx.setCaption('X:')
PetPositionFeetx.Font.Color = 0xffffff
PetPositionFeetx.Font.Size = 8
PetPositionFeetx.Font.Style = ('fsBold')
PetPositionFeetx.Top = 285
PetPositionFeetx.Left = 5
PetPositionWingsx=createLabel(PetModelForm)
PetPositionWingsx.setCaption('X:')
PetPositionWingsx.Font.Color = 0xffffff
PetPositionWingsx.Font.Size = 8
PetPositionWingsx.Font.Style = ('fsBold')
PetPositionWingsx.Top = 355
PetPositionWingsx.Left = 5
PetPositionBackx=createLabel(PetModelForm)
PetPositionBackx.setCaption('X:')
PetPositionBackx.Font.Color = 0xffffff
PetPositionBackx.Font.Size = 8
PetPositionBackx.Font.Style = ('fsBold')
PetPositionBackx.Top = 425
PetPositionBackx.Left = 5
PetPositionCentralBodyx.Visible = false
PetPositionHeadx.Visible = false
PetPositionHandsx.Visible = false
PetPositionFeetx.Visible = false
PetPositionWingsx.Visible = false
PetPositionBackx.Visible = false
PetPositionCentralBodyy=createLabel(PetModelForm)
PetPositionCentralBodyy.setCaption('Y:')
PetPositionCentralBodyy.Font.Color = 0xffffff
PetPositionCentralBodyy.Font.Size = 8
PetPositionCentralBodyy.Font.Style = ('fsBold')
PetPositionCentralBodyy.Top = 75
PetPositionCentralBodyy.Left = 135
PetPositionHeady=createLabel(PetModelForm)
PetPositionHeady.setCaption('Y:')
PetPositionHeady.Font.Color = 0xffffff
PetPositionHeady.Font.Size = 8
PetPositionHeady.Font.Style = ('fsBold')
PetPositionHeady.Top = 145
PetPositionHeady.Left = 135
PetPositionHandsy=createLabel(PetModelForm)
PetPositionHandsy.setCaption('Y:')
PetPositionHandsy.Font.Color = 0xffffff
PetPositionHandsy.Font.Size = 8
PetPositionHandsy.Font.Style = ('fsBold')
PetPositionHandsy.Top = 215
PetPositionHandsy.Left = 135
PetPositionFeety=createLabel(PetModelForm)
PetPositionFeety.setCaption('Y:')
PetPositionFeety.Font.Color = 0xffffff
PetPositionFeety.Font.Size = 8
PetPositionFeety.Font.Style = ('fsBold')
PetPositionFeety.Top = 285
PetPositionFeety.Left = 135
PetPositionWingsy=createLabel(PetModelForm)
PetPositionWingsy.setCaption('Y:')
PetPositionWingsy.Font.Color = 0xffffff
PetPositionWingsy.Font.Size = 8
PetPositionWingsy.Font.Style = ('fsBold')
PetPositionWingsy.Top = 355
PetPositionWingsy.Left = 135
PetPositionBacky=createLabel(PetModelForm)
PetPositionBacky.setCaption('Y:')
PetPositionBacky.Font.Color = 0xffffff
PetPositionBacky.Font.Size = 8
PetPositionBacky.Font.Style = ('fsBold')
PetPositionBacky.Top = 425
PetPositionBacky.Left = 135
PetPositionCentralBodyy.Visible = false
PetPositionHeady.Visible = false
PetPositionHandsy.Visible = false
PetPositionFeety.Visible = false
PetPositionWingsy.Visible = false
PetPositionBacky.Visible = false
PetPositionCentralBodyz=createLabel(PetModelForm)
PetPositionCentralBodyz.setCaption('Z:')
PetPositionCentralBodyz.Font.Color = 0xffffff
PetPositionCentralBodyz.Font.Size = 8
PetPositionCentralBodyz.Font.Style = ('fsBold')
PetPositionCentralBodyz.Top = 75
PetPositionCentralBodyz.Left = 265
PetPositionHeadz=createLabel(PetModelForm)
PetPositionHeadz.setCaption('Z:')
PetPositionHeadz.Font.Color = 0xffffff
PetPositionHeadz.Font.Size = 8
PetPositionHeadz.Font.Style = ('fsBold')
PetPositionHeadz.Top = 150
PetPositionHeadz.Left = 265
PetPositionHandsz=createLabel(PetModelForm)
PetPositionHandsz.setCaption('Z:')
PetPositionHandsz.Font.Color = 0xffffff
PetPositionHandsz.Font.Size = 8
PetPositionHandsz.Font.Style = ('fsBold')
PetPositionHandsz.Top = 225
PetPositionHandsz.Left = 265
PetPositionFeetz=createLabel(PetModelForm)
PetPositionFeetz.setCaption('Z:')
PetPositionFeetz.Font.Color = 0xffffff
PetPositionFeetz.Font.Size = 8
PetPositionFeetz.Font.Style = ('fsBold')
PetPositionFeetz.Top = 300
PetPositionFeetz.Left = 265
PetPositionWingsz=createLabel(PetModelForm)
PetPositionWingsz.setCaption('Z:')
PetPositionWingsz.Font.Color = 0xffffff
PetPositionWingsz.Font.Size = 8
PetPositionWingsz.Font.Style = ('fsBold')
PetPositionWingsz.Top = 375
PetPositionWingsz.Left = 265
PetPositionBackz=createLabel(PetModelForm)
PetPositionBackz.setCaption('Z:')
PetPositionBackz.Font.Color = 0xffffff
PetPositionBackz.Font.Size = 8
PetPositionBackz.Font.Style = ('fsBold')
PetPositionBackz.Top = 425
PetPositionBackz.Left = 320
PetPositionCentralBodyz.Visible = false
PetPositionHeadz.Visible = false
PetPositionHandsz.Visible = false
PetPositionFeetz.Visible = false
PetPositionWingsz.Visible = false
PetPositionBackz.Visible = false
PetHBHeight=createLabel(PetModelForm)
PetHBHeight.setCaption('Height:')
PetHBHeight.Font.Color = 0xffffff
PetHBHeight.Font.Size = 12
PetHBHeight.Font.Style = ('fsUnderline, fsBold')
PetHBHeight.Top = 125
PetHBHeight.Left = 170
PetHBScaleHeight=createLabel(PetModelForm)
PetHBScaleHeight.setCaption('Scale Height:')
PetHBScaleHeight.Font.Color = 0xffffff
PetHBScaleHeight.Font.Size = 12
PetHBScaleHeight.Font.Style = ('fsUnderline, fsBold')
PetHBScaleHeight.Top = 225
PetHBScaleHeight.Left = 150
PetHBScaleWidth=createLabel(PetModelForm)
PetHBScaleWidth.setCaption('Scale Width:')
PetHBScaleWidth.Font.Color = 0xffffff
PetHBScaleWidth.Font.Size = 12
PetHBScaleWidth.Font.Style = ('fsUnderline, fsBold')
PetHBScaleWidth.Top = 325
PetHBScaleWidth.Left = 150
PetHBHeight.Visible = false
PetHBScaleHeight.Visible = false
PetHBScaleWidth.Visible = false
--Actual Value Send/Get--
Petslider.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+92", getProperty(Petslider, 'Position'))
end
PetsliderRefreshTimer = createTimer(getMainForm())
PetsliderRefreshTimer.Interval = 500
PetsliderRefreshTimer.onTimer = function(sender)
  if Petslider.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+92") then
  else
  setProperty(Petslider, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+92"))
 end
end
Petslider2.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+90", getProperty(Petslider2, 'Position'))
end
Petslider2RefreshTimer = createTimer(getMainForm())
Petslider2RefreshTimer.Interval = 500
Petslider2RefreshTimer.onTimer = function(sender)
  if Petslider2.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+90") then
  else
  setProperty(Petslider2, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+90"))
 end
end
Petslider3.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+94", getProperty(Petslider3, 'Position'))
end
Petslider3RefreshTimer = createTimer(getMainForm())
Petslider3RefreshTimer.Interval = 500
Petslider3RefreshTimer.onTimer = function(sender)
  if Petslider3.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+94") then
  else
  setProperty(Petslider3, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+94"))
 end
end
Petslider4.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+96", getProperty(Petslider4, 'Position'))
end
Petslider4RefreshTimer = createTimer(getMainForm())
Petslider4RefreshTimer.Interval = 500
Petslider4RefreshTimer.onTimer = function(sender)
  if Petslider4.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+96") then
  else
  setProperty(Petslider4, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+96"))
 end
end
Petslider5.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+98", getProperty(Petslider5, 'Position'))
end
Petslider5RefreshTimer = createTimer(getMainForm())
Petslider5RefreshTimer.Interval = 500
Petslider5RefreshTimer.onTimer = function(sender)
  if Petslider5.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+98") then
  else
  setProperty(Petslider5, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+98"))
 end
end
Petslider6.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9C", getProperty(Petslider6, 'Position'))
end
Petslider6RefreshTimer = createTimer(getMainForm())
Petslider6RefreshTimer.Interval = 500
Petslider6RefreshTimer.onTimer = function(sender)
  if Petslider6.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9C") then
  else
  setProperty(Petslider6, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9C"))
 end
end
Petslider7.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9A", getProperty(Petslider7, 'Position'))
end
Petslider7RefreshTimer = createTimer(getMainForm())
Petslider7RefreshTimer.Interval = 500
Petslider7RefreshTimer.onTimer = function(sender)
  if Petslider7.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9A") then
  else
  setProperty(Petslider7, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9A"))
 end
end
Petslider8.OnChange = function (sender)
writeSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9E", getProperty(Petslider8, 'Position'))
end
Petslider8RefreshTimer = createTimer(getMainForm())
Petslider8RefreshTimer.Interval = 500
Petslider8RefreshTimer.onTimer = function(sender)
  if Petslider8.position == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9E") then
  else
  setProperty(Petslider8, 'Position', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9E"))
 end
end
PetsliderBS.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A0", getProperty(PetsliderBS, 'Position')*0.01)
end
PetsliderBSRefreshTimer = createTimer(getMainForm())
PetsliderBSRefreshTimer.Interval = 1500
PetsliderBSRefreshTimer.onTimer = function(sender)
  if (PetsliderBS.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A0") then
  elseif tonumber(PetBSedit.Text) ~= nil then
  setProperty(PetsliderBS, 'Position', (round(tonumber(PetBSedit.Text)/0.01)))
 end
end
PetsliderBS2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A4", getProperty(PetsliderBS2, 'Position')*0.01)
end
PetsliderBS2RefreshTimer = createTimer(getMainForm())
PetsliderBS2RefreshTimer.Interval = 1500
PetsliderBS2RefreshTimer.onTimer = function(sender)
  if (PetsliderBS2.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A4") then
  elseif tonumber(PetBSedit2.Text) ~= nil then
  setProperty(PetsliderBS2, 'Position', (round(tonumber(PetBSedit2.Text)/0.01)))
 end
end
PetsliderBS3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A8", getProperty(PetsliderBS3, 'Position')*0.01)
end
PetsliderBS3RefreshTimer = createTimer(getMainForm())
PetsliderBS3RefreshTimer.Interval = 1500
PetsliderBS3RefreshTimer.onTimer = function(sender)
  if (PetsliderBS3.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A8") then
  elseif tonumber(PetBSedit3.Text) ~= nil then
  setProperty(PetsliderBS3, 'Position', (round(tonumber(PetBSedit3.Text)/0.01)))
 end
end
PetsliderBS4.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+AC", getProperty(PetsliderBS4, 'Position')*0.01)
end
PetsliderBS4RefreshTimer = createTimer(getMainForm())
PetsliderBS4RefreshTimer.Interval = 1500
PetsliderBS4RefreshTimer.onTimer = function(sender)
  if (PetsliderBS4.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+AC") then
  elseif tonumber(PetBSedit4.Text) ~= nil then
  setProperty(PetsliderBS4, 'Position', (round(tonumber(PetBSedit4.Text)/0.01)))
 end
end
PetsliderBS5.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B0", getProperty(PetsliderBS5, 'Position')*0.01)
end
PetsliderBS5RefreshTimer = createTimer(getMainForm())
PetsliderBS5RefreshTimer.Interval = 1500
PetsliderBS5RefreshTimer.onTimer = function(sender)
  if (PetsliderBS5.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B0") then
  elseif tonumber(PetBSedit5.Text) ~= nil then
  setProperty(PetsliderBS5, 'Position', (round(tonumber(PetBSedit5.Text)/0.01)))
 end
end
PetsliderBS6.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B8", getProperty(PetsliderBS6, 'Position')*0.01)
end
PetsliderBS6RefreshTimer = createTimer(getMainForm())
PetsliderBS6RefreshTimer.Interval = 1500
PetsliderBS6RefreshTimer.onTimer = function(sender)
  if (PetsliderBS6.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B8") then
  elseif tonumber(PetBSedit6.Text) ~= nil then
  setProperty(PetsliderBS6, 'Position', (round(tonumber(PetBSedit6.Text)/0.01)))
 end
end
PetsliderBS7.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C0", getProperty(PetsliderBS7, 'Position')*0.01)
end
PetsliderBS7RefreshTimer = createTimer(getMainForm())
PetsliderBS7RefreshTimer.Interval = 1500
PetsliderBS7RefreshTimer.onTimer = function(sender)
  if (PetsliderBS7.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C0") then
  elseif tonumber(PetBSedit7.Text) ~= nil then
  setProperty(PetsliderBS7, 'Position', (round(tonumber(PetBSedit7.Text)/0.01)))
 end
end
PetsliderBS8.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B4", getProperty(PetsliderBS8, 'Position')*0.01)
end
PetsliderBS8RefreshTimer = createTimer(getMainForm())
PetsliderBS8RefreshTimer.Interval = 1500
PetsliderBS8RefreshTimer.onTimer = function(sender)
  if (PetsliderBS8.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B4") then
  elseif tonumber(PetBSedit8.Text) ~= nil then
  setProperty(PetsliderBS8, 'Position', (round(tonumber(PetBSedit8.Text)/0.01)))
 end
end
PetsliderBR2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C4", getProperty(PetsliderBR2, 'Position'))
end
PetsliderBR2RefreshTimer = createTimer(getMainForm())
PetsliderBR2RefreshTimer.Interval = 500
PetsliderBR2RefreshTimer.onTimer = function(sender)
  if PetsliderBR2.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C4") then
  else
  setProperty(PetsliderBR2, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C4"))
 end
end
PetsliderBR3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C8", getProperty(PetsliderBR3, 'Position'))
end
PetsliderBR3RefreshTimer = createTimer(getMainForm())
PetsliderBR3RefreshTimer.Interval = 500
PetsliderBR3RefreshTimer.onTimer = function(sender)
  if PetsliderBR3.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C8") then
  else
  setProperty(PetsliderBR3, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C8"))
 end
end
PetsliderBR4.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+CC", getProperty(PetsliderBR4, 'Position'))
end
PetsliderBR4RefreshTimer = createTimer(getMainForm())
PetsliderBR4RefreshTimer.Interval = 500
PetsliderBR4RefreshTimer.onTimer = function(sender)
  if PetsliderBR4.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+CC") then
  else
  setProperty(PetsliderBR4, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+CC"))
 end
end
PetsliderBR5.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D0", getProperty(PetsliderBR5, 'Position'))
end
PetsliderBR5RefreshTimer = createTimer(getMainForm())
PetsliderBR5RefreshTimer.Interval = 500
PetsliderBR5RefreshTimer.onTimer = function(sender)
  if PetsliderBR5.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D0") then
  else
  setProperty(PetsliderBR5, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D0"))
 end
end
PetsliderBR6.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D4", getProperty(PetsliderBR6, 'Position'))
end
PetsliderBR6RefreshTimer = createTimer(getMainForm())
PetsliderBR6RefreshTimer.Interval = 500
PetsliderBR6RefreshTimer.onTimer = function(sender)
  if PetsliderBR6.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D4") then
  else
  setProperty(PetsliderBR6, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D4"))
 end
end
PetsliderBR7.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D8", getProperty(PetsliderBR7, 'Position'))
end
PetsliderBR7RefreshTimer = createTimer(getMainForm())
PetsliderBR7RefreshTimer.Interval = 500
PetsliderBR7RefreshTimer.onTimer = function(sender)
  if PetsliderBR7.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D8") then
  else
  setProperty(PetsliderBR7, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D8"))
 end
end
PetsliderBR8.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+DC", getProperty(PetsliderBR8, 'Position'))
end
PetsliderBR8RefreshTimer = createTimer(getMainForm())
PetsliderBR8RefreshTimer.Interval = 500
PetsliderBR8RefreshTimer.onTimer = function(sender)
  if PetsliderBR8.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+DC") then
  else
  setProperty(PetsliderBR8, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+DC"))
 end
end
PetsliderBPX.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E0", getProperty(PetsliderBPX, 'Position'))
end
PetsliderBPXRefreshTimer = createTimer(getMainForm())
PetsliderBPXRefreshTimer.Interval = 500
PetsliderBPXRefreshTimer.onTimer = function(sender)
  if PetsliderBPX.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E0") then
  else
  setProperty(PetsliderBPX, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E0"))
 end
end
PetsliderBPX2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+EC", getProperty(PetsliderBPX2, 'Position'))
end
PetsliderBPX2RefreshTimer = createTimer(getMainForm())
PetsliderBPX2RefreshTimer.Interval = 500
PetsliderBPX2RefreshTimer.onTimer = function(sender)
  if PetsliderBPX2.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+EC") then
  else
  setProperty(PetsliderBPX2, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+EC"))
 end
end
PetsliderBPX3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F8", getProperty(PetsliderBPX3, 'Position'))
end
PetsliderBPX3RefreshTimer = createTimer(getMainForm())
PetsliderBPX3RefreshTimer.Interval = 500
PetsliderBPX3RefreshTimer.onTimer = function(sender)
  if PetsliderBPX3.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F8") then
  else
  setProperty(PetsliderBPX3, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F8"))
 end
end
PetsliderBPX4.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+104", getProperty(PetsliderBPX4, 'Position'))
end
PetsliderBPX4RefreshTimer = createTimer(getMainForm())
PetsliderBPX4RefreshTimer.Interval = 500
PetsliderBPX4RefreshTimer.onTimer = function(sender)
  if PetsliderBPX4.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+104") then
  else
  setProperty(PetsliderBPX4, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+104"))
 end
end
PetsliderBPX5.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+11C", getProperty(PetsliderBPX5, 'Position'))
end
PetsliderBPX5RefreshTimer = createTimer(getMainForm())
PetsliderBPX5RefreshTimer.Interval = 500
PetsliderBPX5RefreshTimer.onTimer = function(sender)
  if PetsliderBPX5.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+11C") then
  else
  setProperty(PetsliderBPX5, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+11C"))
 end
end
PetsliderBPX6.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+110", getProperty(PetsliderBPX6, 'Position'))
end
PetsliderBPX6RefreshTimer = createTimer(getMainForm())
PetsliderBPX6RefreshTimer.Interval = 500
PetsliderBPX6RefreshTimer.onTimer = function(sender)
  if PetsliderBPX6.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+110") then
  else
  setProperty(PetsliderBPX6, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+110"))
 end
end
PetsliderBPY1.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E8", getProperty(PetsliderBPY1, 'Position'))
end
PetsliderBPY1RefreshTimer = createTimer(getMainForm())
PetsliderBPY1RefreshTimer.Interval = 500
PetsliderBPY1RefreshTimer.onTimer = function(sender)
  if PetsliderBPY1.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E8") then
  else
  setProperty(PetsliderBPY1, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E8"))
 end
end
PetsliderBPY2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F4", getProperty(PetsliderBPY2, 'Position'))
end
PetsliderBPY2RefreshTimer = createTimer(getMainForm())
PetsliderBPY2RefreshTimer.Interval = 500
PetsliderBPY2RefreshTimer.onTimer = function(sender)
  if PetsliderBPY2.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F4") then
  else
  setProperty(PetsliderBPY2, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F4"))
 end
end
PetsliderBPY3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+100", getProperty(PetsliderBPY3, 'Position'))
end
PetsliderBPY3RefreshTimer = createTimer(getMainForm())
PetsliderBPY3RefreshTimer.Interval = 500
PetsliderBPY3RefreshTimer.onTimer = function(sender)
  if PetsliderBPY3.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+100") then
  else
  setProperty(PetsliderBPY3, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+100"))
 end
end
PetsliderBPY4.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+10C", getProperty(PetsliderBPY4, 'Position'))
end
PetsliderBPY4RefreshTimer = createTimer(getMainForm())
PetsliderBPY4RefreshTimer.Interval = 500
PetsliderBPY4RefreshTimer.onTimer = function(sender)
  if PetsliderBPY4.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+10C") then
  else
  setProperty(PetsliderBPY4, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+10C"))
 end
end
PetsliderBPY5.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+124", getProperty(PetsliderBPY5, 'Position'))
end
PetsliderBPY5RefreshTimer = createTimer(getMainForm())
PetsliderBPY5RefreshTimer.Interval = 500
PetsliderBPY5RefreshTimer.onTimer = function(sender)
  if PetsliderBPY5.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+124") then
  else
  setProperty(PetsliderBPY5, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+124"))
 end
end
PetsliderBPY6.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+118", getProperty(PetsliderBPY6, 'Position'))
end
PetsliderBPY6RefreshTimer = createTimer(getMainForm())
PetsliderBPY6RefreshTimer.Interval = 500
PetsliderBPY6RefreshTimer.onTimer = function(sender)
  if PetsliderBPY6.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+118") then
  else
  setProperty(PetsliderBPY6, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+118"))
 end
end
PetsliderBPZ1.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E4", getProperty(PetsliderBPZ1, 'Position'))
end
PetsliderBPZ1RefreshTimer = createTimer(getMainForm())
PetsliderBPZ1RefreshTimer.Interval = 500
PetsliderBPZ1RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ1.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E4") then
  else
  setProperty(PetsliderBPZ1, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E4"))
 end
end
PetsliderBPZ2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F0", getProperty(PetsliderBPZ2, 'Position'))
end
PetsliderBPZ2RefreshTimer = createTimer(getMainForm())
PetsliderBPZ2RefreshTimer.Interval = 500
PetsliderBPZ2RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ2.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F0") then
  else
  setProperty(PetsliderBPZ2, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F0"))
 end
end
PetsliderBPZ3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+FC", getProperty(PetsliderBPZ3, 'Position'))
end
PetsliderBPZ3RefreshTimer = createTimer(getMainForm())
PetsliderBPZ3RefreshTimer.Interval = 500
PetsliderBPZ3RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ3.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+FC") then
  else
  setProperty(PetsliderBPZ3, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+FC"))
 end
end
PetsliderBPZ4.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+108", getProperty(PetsliderBPZ4, 'Position'))
end
PetsliderBPZ4RefreshTimer = createTimer(getMainForm())
PetsliderBPZ4RefreshTimer.Interval = 500
PetsliderBPZ4RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ4.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+108") then
  else
  setProperty(PetsliderBPZ4, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+108"))
 end
end
PetsliderBPZ5.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+120", getProperty(PetsliderBPZ5, 'Position'))
end
PetsliderBPZ5RefreshTimer = createTimer(getMainForm())
PetsliderBPZ5RefreshTimer.Interval = 500
PetsliderBPZ5RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ5.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+120") then
  else
  setProperty(PetsliderBPZ5, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+120"))
 end
end
PetsliderBPZ6.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+114", getProperty(PetsliderBPZ6, 'Position'))
end
PetsliderBPZ6RefreshTimer = createTimer(getMainForm())
PetsliderBPZ6RefreshTimer.Interval = 500
PetsliderBPZ6RefreshTimer.onTimer = function(sender)
  if PetsliderBPZ6.position == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+114") then
  else
  setProperty(PetsliderBPZ6, 'Position', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+114"))
 end
end
PetsliderHB.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+8C", getProperty(PetsliderHB, 'Position')*0.01)
end
PetsliderHBRefreshTimer = createTimer(getMainForm())
PetsliderHBRefreshTimer.Interval = 5000
PetsliderHBRefreshTimer.onTimer = function(sender)
  if (PetsliderHB.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+8C") then
  elseif tonumber(PetHBedit.Text) ~= nil then
  setProperty(PetsliderHB, 'Position', (round(tonumber(PetHBedit.Text)/0.01)))
 end
end
PetsliderHB2.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+88", getProperty(PetsliderHB2, 'Position')*0.01)
end
PetsliderHB2RefreshTimer = createTimer(getMainForm())
PetsliderHB2RefreshTimer.Interval = 5000
PetsliderHB2RefreshTimer.onTimer = function(sender)
  if (PetsliderHB2.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+88") then
  elseif tonumber(PetHBedit2.Text) ~= nil then
  setProperty(PetsliderHB2, 'Position', (round(tonumber(PetHBedit2.Text)/0.01)))
 end
end
PetsliderHB3.OnChange = function (sender)
writeFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+84", getProperty(PetsliderHB3, 'Position')*0.01)
end
PetsliderHB3RefreshTimer = createTimer(getMainForm())
PetsliderHB3RefreshTimer.Interval = 5000
PetsliderHB3RefreshTimer.onTimer = function(sender)
  if (PetsliderHB3.position*0.01) == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+84") then
  elseif tonumber(PetHBedit3.Text) ~= nil then
  setProperty(PetsliderHB3, 'Position', (round(tonumber(PetHBedit3.Text)/0.01)))
 end
end

PetModelForm.OnClose = function(sender)
   checkbox_setState(PetModelButton, 0)
   return caHide
end
PetModelButton.OnChange = function(sender)
  if(checkbox_getState(PetModelButton) == 1) then
PetModelForm.show()
  elseif (checkbox_getState(PetModelButton) == 0) then
PetModelForm.hide()
  end
end
--PetModelEditBox
PetMainedit=createEdit(PetModelForm)
PetMainedit.Top = 50
PetMainedit.Left = 350
PetMainedit.Width = 40
PetMaineditRefreshTimer1 = createTimer(getMainForm())
PetMaineditRefreshTimer1.Interval = 500
PetMaineditRefreshTimer1.onTimer = function(sender)
  if PetMainedit.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+92") then
  else
  setProperty(PetMainedit, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+92"))
 end
end
PetMainedit2=createEdit(PetModelForm)
PetMainedit2.Top = 100
PetMainedit2.Left = 350
PetMainedit2.Width = 40
PetMaineditRefreshTimer2 = createTimer(getMainForm())
PetMaineditRefreshTimer2.Interval = 500
PetMaineditRefreshTimer2.onTimer = function(sender)
  if PetMainedit2.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+90") then
  else
  setProperty(PetMainedit2, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+90"))
 end
end
PetMainedit3=createEdit(PetModelForm)
PetMainedit3.Top = 150
PetMainedit3.Left = 350
PetMainedit3.Width = 40
PetMaineditRefreshTimer3 = createTimer(getMainForm())
PetMaineditRefreshTimer3.Interval = 500
PetMaineditRefreshTimer3.onTimer = function(sender)
  if PetMainedit3.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+94") then
  else
  setProperty(PetMainedit3, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+94"))
 end
end
PetMainedit4=createEdit(PetModelForm)
PetMainedit4.Top = 200
PetMainedit4.Left = 350
PetMainedit4.Width = 40
PetMaineditRefreshTimer4 = createTimer(getMainForm())
PetMaineditRefreshTimer4.Interval = 500
PetMaineditRefreshTimer4.onTimer = function(sender)
  if PetMainedit4.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+96") then
  else
  setProperty(PetMainedit4, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+96"))
 end
end
PetMainedit5=createEdit(PetModelForm)
PetMainedit5.Top = 250
PetMainedit5.Left = 350
PetMainedit5.Width = 40
PetMaineditRefreshTimer5 = createTimer(getMainForm())
PetMaineditRefreshTimer5.Interval = 500
PetMaineditRefreshTimer5.onTimer = function(sender)
  if PetMainedit5.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+98") then
  else
  setProperty(PetMainedit5, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+98"))
 end
end
PetMainedit6=createEdit(PetModelForm)
PetMainedit6.Top = 300
PetMainedit6.Left = 350
PetMainedit6.Width = 40
PetMaineditRefreshTimer6 = createTimer(getMainForm())
PetMaineditRefreshTimer6.Interval = 500
PetMaineditRefreshTimer6.onTimer = function(sender)
  if PetMainedit6.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9C") then
  else
  setProperty(PetMainedit6, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9C"))
 end
end
PetMainedit7=createEdit(PetModelForm)
PetMainedit7.Top = 350
PetMainedit7.Left = 350
PetMainedit7.Width = 40
PetMaineditRefreshTimer7 = createTimer(getMainForm())
PetMaineditRefreshTimer7.Interval = 500
PetMaineditRefreshTimer7.onTimer = function(sender)
  if PetMainedit7.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9A") then
  else
  setProperty(PetMainedit7, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9A"))
 end
end
PetMainedit8=createEdit(PetModelForm)
PetMainedit8.Top = 400
PetMainedit8.Left = 350
PetMainedit8.Width = 40
PetMaineditRefreshTimer8 = createTimer(getMainForm())
PetMaineditRefreshTimer8.Interval = 500
PetMaineditRefreshTimer8.onTimer = function(sender)
  if PetMainedit8.text == readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9E") then
  else
  setProperty(PetMainedit8, 'text', readSmallInteger("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+9E"))
 end
end
PetBSedit=createEdit(PetModelForm)
PetBSedit.Top = 50
PetBSedit.Left = 350
PetBSedit.Width = 40
PetBSeditRefreshTimer = createTimer(getMainForm())
PetBSeditRefreshTimer.Interval = 500
PetBSeditRefreshTimer.onTimer = function(sender)
  if PetBSedit.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A0") then
  else
  setProperty(PetBSedit, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A0"))
 end
end
PetBSedit2=createEdit(PetModelForm)
PetBSedit2.Top = 100
PetBSedit2.Left = 350
PetBSedit2.Width = 40
PetBSeditRefreshTimer2 = createTimer(getMainForm())
PetBSeditRefreshTimer2.Interval = 500
PetBSeditRefreshTimer2.onTimer = function(sender)
  if PetBSedit2.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A4") then
  else
  setProperty(PetBSedit2, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A4"))
 end
 end
PetBSedit3=createEdit(PetModelForm)
PetBSedit3.Top = 150
PetBSedit3.Left = 350
PetBSedit3.Width = 40
PetBSeditRefreshTimer3 = createTimer(getMainForm())
PetBSeditRefreshTimer3.Interval = 500
PetBSeditRefreshTimer3.onTimer = function(sender)
  if PetBSedit3.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A8") then
  else
  setProperty(PetBSedit3, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+A8"))
 end
 end
PetBSedit4=createEdit(PetModelForm)
PetBSedit4.Top = 200
PetBSedit4.Left = 350
PetBSedit4.Width = 40
PetBSeditRefreshTimer4 = createTimer(getMainForm())
PetBSeditRefreshTimer4.Interval = 500
PetBSeditRefreshTimer4.onTimer = function(sender)
  if PetBSedit4.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+AC") then
  else
  setProperty(PetBSedit4, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+AC"))
 end
 end
PetBSedit5=createEdit(PetModelForm)
PetBSedit5.Top = 250
PetBSedit5.Left = 350
PetBSedit5.Width = 40
PetBSeditRefreshTimer5 = createTimer(getMainForm())
PetBSeditRefreshTimer5.Interval = 500
PetBSeditRefreshTimer5.onTimer = function(sender)
  if PetBSedit5.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B0") then
  else
  setProperty(PetBSedit5, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B0"))
 end
 end
PetBSedit6=createEdit(PetModelForm)
PetBSedit6.Top = 300
PetBSedit6.Left = 350
PetBSedit6.Width = 40
PetBSeditRefreshTimer6 = createTimer(getMainForm())
PetBSeditRefreshTimer6.Interval = 500
PetBSeditRefreshTimer6.onTimer = function(sender)
  if PetBSedit6.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B8") then
  else
  setProperty(PetBSedit6, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B8"))
 end
 end
PetBSedit7=createEdit(PetModelForm)
PetBSedit7.Top = 350
PetBSedit7.Left = 350
PetBSedit7.Width = 40
PetBSeditRefreshTimer7 = createTimer(getMainForm())
PetBSeditRefreshTimer7.Interval = 500
PetBSeditRefreshTimer7.onTimer = function(sender)
  if PetBSedit7.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C0") then
  else
  setProperty(PetBSedit7, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C0"))
 end
 end
PetBSedit8=createEdit(PetModelForm)
PetBSedit8.Top = 400
PetBSedit8.Left = 350
PetBSedit8.Width = 40
PetBSeditRefreshTimer8 = createTimer(getMainForm())
PetBSeditRefreshTimer8.Interval = 500
PetBSeditRefreshTimer8.onTimer = function(sender)
  if PetBSedit8.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B4") then
  else
  setProperty(PetBSedit8, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+B4"))
 end
 end
PetBSedit.Visible = false
PetBSedit2.Visible = false
PetBSedit3.Visible = false
PetBSedit4.Visible = false
PetBSedit5.Visible = false
PetBSedit6.Visible = false
PetBSedit7.Visible = false
PetBSedit8.Visible = false
PetBRedit2=createEdit(PetModelForm)
PetBRedit2.Top = 100
PetBRedit2.Left = 350
PetBRedit2.Width = 40
PetBReditRefreshTimer2 = createTimer(getMainForm())
PetBReditRefreshTimer2.Interval = 500
PetBReditRefreshTimer2.onTimer = function(sender)
  if PetBRedit2.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C4") then
  else
  setProperty(PetBRedit2, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C4"))
 end
 end
PetBRedit3=createEdit(PetModelForm)
PetBRedit3.Top = 150
PetBRedit3.Left = 350
PetBRedit3.Width = 40
PetBReditRefreshTimer3 = createTimer(getMainForm())
PetBReditRefreshTimer3.Interval = 500
PetBReditRefreshTimer3.onTimer = function(sender)
  if PetBRedit3.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C8") then
  else
  setProperty(PetBRedit3, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+C8"))
 end
 end
PetBRedit4=createEdit(PetModelForm)
PetBRedit4.Top = 200
PetBRedit4.Left = 350
PetBRedit4.Width = 40
PetBReditRefreshTimer4 = createTimer(getMainForm())
PetBReditRefreshTimer4.Interval = 500
PetBReditRefreshTimer4.onTimer = function(sender)
  if PetBRedit4.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+CC") then
  else
  setProperty(PetBRedit4, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+CC"))
 end
 end
PetBRedit5=createEdit(PetModelForm)
PetBRedit5.Top = 250
PetBRedit5.Left = 350
PetBRedit5.Width = 40
PetBReditRefreshTimer5 = createTimer(getMainForm())
PetBReditRefreshTimer5.Interval = 500
PetBReditRefreshTimer5.onTimer = function(sender)
  if PetBRedit5.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D0") then
  else
  setProperty(PetBRedit5, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D0"))
 end
 end
PetBRedit6=createEdit(PetModelForm)
PetBRedit6.Top = 300
PetBRedit6.Left = 350
PetBRedit6.Width = 40
PetBReditRefreshTimer6 = createTimer(getMainForm())
PetBReditRefreshTimer6.Interval = 500
PetBReditRefreshTimer6.onTimer = function(sender)
  if PetBRedit6.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D4") then
  else
  setProperty(PetBRedit6, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D4"))
 end
 end
PetBRedit7=createEdit(PetModelForm)
PetBRedit7.Top = 350
PetBRedit7.Left = 350
PetBRedit7.Width = 40
PetBReditRefreshTimer7 = createTimer(getMainForm())
PetBReditRefreshTimer7.Interval = 500
PetBReditRefreshTimer7.onTimer = function(sender)
  if PetBRedit7.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D8") then
  else
  setProperty(PetBRedit7, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+D8"))
 end
 end
PetBRedit8=createEdit(PetModelForm)
PetBRedit8.Top = 400
PetBRedit8.Left = 350
PetBRedit8.Width = 40
PetBReditRefreshTimer8 = createTimer(getMainForm())
PetBReditRefreshTimer8.Interval = 500
PetBReditRefreshTimer8.onTimer = function(sender)
  if PetBRedit8.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+DC") then
  else
  setProperty(PetBRedit8, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+DC"))
 end
 end
PetBRedit2.Visible = false
PetBRedit3.Visible = false
PetBRedit4.Visible = false
PetBRedit5.Visible = false
PetBRedit6.Visible = false
PetBRedit7.Visible = false
PetBRedit8.Visible = false
PetBPeditX2=createEdit(PetModelForm)
PetBPeditX2.Top = 50
PetBPeditX2.Left = 50
PetBPeditX2.Width = 45
PetBPeditRefreshTimerX2 = createTimer(getMainForm())
PetBPeditRefreshTimerX2.Interval = 500
PetBPeditRefreshTimerX2.onTimer = function(sender)
  if PetBPeditX2.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E0") then
  else
  setProperty(PetBPeditX2, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E0"))
 end
 end
PetBPeditX3=createEdit(PetModelForm)
PetBPeditX3.Top = 120
PetBPeditX3.Left = 50
PetBPeditX3.Width = 45
PetBPeditRefreshTimerX3 = createTimer(getMainForm())
PetBPeditRefreshTimerX3.Interval = 500
PetBPeditRefreshTimerX3.onTimer = function(sender)
  if PetBPeditX3.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+EC") then
  else
  setProperty(PetBPeditX3, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+EC"))
 end
 end
PetBPeditX4=createEdit(PetModelForm)
PetBPeditX4.Top = 190
PetBPeditX4.Left = 50
PetBPeditX4.Width = 45
PetBPeditRefreshTimerX4 = createTimer(getMainForm())
PetBPeditRefreshTimerX4.Interval = 500
PetBPeditRefreshTimerX4.onTimer = function(sender)
  if PetBPeditX4.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F8") then
  else
  setProperty(PetBPeditX4, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F8"))
 end
 end
PetBPeditX5=createEdit(PetModelForm)
PetBPeditX5.Top = 260
PetBPeditX5.Left = 50
PetBPeditX5.Width = 45
PetBPeditRefreshTimerX5 = createTimer(getMainForm())
PetBPeditRefreshTimerX5.Interval = 500
PetBPeditRefreshTimerX5.onTimer = function(sender)
  if PetBPeditX5.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+104") then
  else
  setProperty(PetBPeditX5, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+104"))
 end
 end
PetBPeditX6=createEdit(PetModelForm)
PetBPeditX6.Top = 330
PetBPeditX6.Left = 50
PetBPeditX6.Width = 45
PetBPeditRefreshTimerX6 = createTimer(getMainForm())
PetBPeditRefreshTimerX6.Interval = 500
PetBPeditRefreshTimerX6.onTimer = function(sender)
  if PetBPeditX6.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+11C") then
  else
  setProperty(PetBPeditX6, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+11C"))
 end
 end
PetBPeditX7=createEdit(PetModelForm)
PetBPeditX7.Top = 400
PetBPeditX7.Left = 50
PetBPeditX7.Width = 45
PetBPeditRefreshTimerX7 = createTimer(getMainForm())
PetBPeditRefreshTimerX7.Interval = 500
PetBPeditRefreshTimerX7.onTimer = function(sender)
  if PetBPeditX7.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+110") then
  else
  setProperty(PetBPeditX7, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+110"))
 end
 end
PetBPeditY2=createEdit(PetModelForm)
PetBPeditY2.Top = 50
PetBPeditY2.Left = 180
PetBPeditY2.Width = 45
PetBPeditRefreshTimerY2 = createTimer(getMainForm())
PetBPeditRefreshTimerY2.Interval = 500
PetBPeditRefreshTimerY2.onTimer = function(sender)
  if PetBPeditY2.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E8") then
  else
  setProperty(PetBPeditY2, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E8"))
 end
 end
PetBPeditY3=createEdit(PetModelForm)
PetBPeditY3.Top = 120
PetBPeditY3.Left = 180
PetBPeditY3.Width = 45
PetBPeditRefreshTimerY3 = createTimer(getMainForm())
PetBPeditRefreshTimerY3.Interval = 500
PetBPeditRefreshTimerY3.onTimer = function(sender)
  if PetBPeditY3.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F4") then
  else
  setProperty(PetBPeditY3, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F4"))
 end
 end
PetBPeditY4=createEdit(PetModelForm)
PetBPeditY4.Top = 190
PetBPeditY4.Left = 180
PetBPeditY4.Width = 45
PetBPeditRefreshTimerY4 = createTimer(getMainForm())
PetBPeditRefreshTimerY4.Interval = 500
PetBPeditRefreshTimerY4.onTimer = function(sender)
  if PetBPeditY4.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+100") then
  else
  setProperty(PetBPeditY4, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+100"))
 end
end
PetBPeditY5=createEdit(PetModelForm)
PetBPeditY5.Top = 260
PetBPeditY5.Left = 180
PetBPeditY5.Width = 45
PetBPeditRefreshTimerY5 = createTimer(getMainForm())
PetBPeditRefreshTimerY5.Interval = 500
PetBPeditRefreshTimerY5.onTimer = function(sender)
  if PetBPeditY5.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+10C") then
  else
  setProperty(PetBPeditY5, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+10C"))
 end
end
PetBPeditY6=createEdit(PetModelForm)
PetBPeditY6.Top = 330
PetBPeditY6.Left = 180
PetBPeditY6.Width = 45
PetBPeditRefreshTimerY6 = createTimer(getMainForm())
PetBPeditRefreshTimerY6.Interval = 500
PetBPeditRefreshTimerY6.onTimer = function(sender)
  if PetBPeditY6.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+124") then
  else
  setProperty(PetBPeditY6, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+124"))
 end
end
PetBPeditY7=createEdit(PetModelForm)
PetBPeditY7.Top = 400
PetBPeditY7.Left = 180
PetBPeditY7.Width = 45
PetBPeditRefreshTimerY7 = createTimer(getMainForm())
PetBPeditRefreshTimerY7.Interval = 500
PetBPeditRefreshTimerY7.onTimer = function(sender)
  if PetBPeditY7.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+118") then
  else
  setProperty(PetBPeditY7, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+118"))
 end
end
PetBPeditZ2=createEdit(PetModelForm)
PetBPeditZ2.Top = 50
PetBPeditZ2.Left = 310
PetBPeditZ2.Width = 45
PetBPeditRefreshTimerZ2 = createTimer(getMainForm())
PetBPeditRefreshTimerZ2.Interval = 500
PetBPeditRefreshTimerZ2.onTimer = function(sender)
  if PetBPeditZ2.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E4") then
  else
  setProperty(PetBPeditZ2, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+E4"))
 end
end
PetBPeditZ3=createEdit(PetModelForm)
PetBPeditZ3.Top = 120
PetBPeditZ3.Left = 310
PetBPeditZ3.Width = 45
PetBPeditRefreshTimerZ3 = createTimer(getMainForm())
PetBPeditRefreshTimerZ3.Interval = 500
PetBPeditRefreshTimerZ3.onTimer = function(sender)
  if PetBPeditZ3.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F0") then
  else
  setProperty(PetBPeditZ3, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+F0"))
 end
end
PetBPeditZ4=createEdit(PetModelForm)
PetBPeditZ4.Top = 190
PetBPeditZ4.Left = 310
PetBPeditZ4.Width = 45
PetBPeditZ4.Height = 15
PetBPeditRefreshTimerZ4 = createTimer(getMainForm())
PetBPeditRefreshTimerZ4.Interval = 500
PetBPeditRefreshTimerZ4.onTimer = function(sender)
  if PetBPeditZ4.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+FC") then
  else
  setProperty(PetBPeditZ4, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+FC"))
 end
end
PetBPeditZ5=createEdit(PetModelForm)
PetBPeditZ5.Top = 260
PetBPeditZ5.Left = 310
PetBPeditZ5.Width = 45
PetBPeditRefreshTimerZ5 = createTimer(getMainForm())
PetBPeditRefreshTimerZ5.Interval = 500
PetBPeditRefreshTimerZ5.onTimer = function(sender)
  if PetBPeditZ5.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+108") then
  else
  setProperty(PetBPeditZ5, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+108"))
 end
end
PetBPeditZ6=createEdit(PetModelForm)
PetBPeditZ6.Top = 330
PetBPeditZ6.Left = 310
PetBPeditZ6.Width = 45
PetBPeditRefreshTimerZ6 = createTimer(getMainForm())
PetBPeditRefreshTimerZ6.Interval = 500
PetBPeditRefreshTimerZ6.onTimer = function(sender)
  if PetBPeditZ6.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+120") then
  else
  setProperty(PetBPeditZ6, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+120"))
 end
end
PetBPeditZ7=createEdit(PetModelForm)
PetBPeditZ7.Top = 400
PetBPeditZ7.Left = 310
PetBPeditZ7.Width = 45
PetBPeditRefreshTimerZ7 = createTimer(getMainForm())
PetBPeditRefreshTimerZ7.Interval = 500
PetBPeditRefreshTimerZ7.onTimer = function(sender)
  if PetBPeditZ7.text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+114") then
  else
  setProperty(PetBPeditZ7, 'text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+114"))
 end
end
PetBPeditX2.Visible = false
PetBPeditX3.Visible = false
PetBPeditX4.Visible = false
PetBPeditX5.Visible = false
PetBPeditX6.Visible = false
PetBPeditX7.Visible = false
PetBPeditY2.Visible = false
PetBPeditY3.Visible = false
PetBPeditY4.Visible = false
PetBPeditY5.Visible = false
PetBPeditY6.Visible = false
PetBPeditY7.Visible = false
PetBPeditZ2.Visible = false
PetBPeditZ3.Visible = false
PetBPeditZ4.Visible = false
PetBPeditZ5.Visible = false
PetBPeditZ6.Visible = false
PetBPeditZ7.Visible = false
PetHBedit=createEdit(PetModelForm)
PetHBedit.Top = 175
PetHBedit.Left = 180
PetHBedit.Width = 35
PetHBeditRefreshTimer = createTimer(getMainForm())
PetHBeditRefreshTimer.Interval = 500
PetHBeditRefreshTimer.onTimer = function(sender)
  if PetHBedit.Text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+8C") then
  else
  setProperty(PetHBedit, 'Text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+8C"))
 end
end
PetHBedit2=createEdit(PetModelForm)
PetHBedit2.Top = 275
PetHBedit2.Left = 180
PetHBedit2.Width = 35
PetHBeditRefreshTimer2 = createTimer(getMainForm())
PetHBeditRefreshTimer2.Interval = 500
PetHBeditRefreshTimer2.onTimer = function(sender)
  if PetHBedit2.Text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+88") then
  else
  setProperty(PetHBedit2, 'Text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+88"))
 end
end
PetHBedit3=createEdit(PetModelForm)
PetHBedit3.Top = 375
PetHBedit3.Left = 180
PetHBedit3.Width = 35
PetHBeditRefreshTimer3 = createTimer(getMainForm())
PetHBeditRefreshTimer3.Interval = 500
PetHBeditRefreshTimer3.onTimer = function(sender)
  if PetHBedit3.Text == readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+84") then
  else
  setProperty(PetHBedit3, 'Text', readFloat("[[[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+88]+0]+28]+84"))
 end
end
PetHBedit.Visible = false
PetHBedit2.Visible = false
PetHBedit3.Visible = false
--OnTopEdit
PetOnTopMainedit=createEdit(PetModelForm)
PetOnTopMainedit.Top = 50
PetOnTopMainedit.Left = 350
PetOnTopMainedit.Width = 40
PetOnTopMainedit2=createEdit(PetModelForm)
PetOnTopMainedit2.Top = 100
PetOnTopMainedit2.Left = 350
PetOnTopMainedit2.Width = 40
PetOnTopMainedit3=createEdit(PetModelForm)
PetOnTopMainedit3.Top = 150
PetOnTopMainedit3.Left = 350
PetOnTopMainedit3.Width = 40
PetOnTopMainedit4=createEdit(PetModelForm)
PetOnTopMainedit4.Top = 200
PetOnTopMainedit4.Left = 350
PetOnTopMainedit4.Width = 40
PetOnTopMainedit5=createEdit(PetModelForm)
PetOnTopMainedit5.Top = 250
PetOnTopMainedit5.Left = 350
PetOnTopMainedit5.Width = 40
PetOnTopMainedit6=createEdit(PetModelForm)
PetOnTopMainedit6.Top = 300
PetOnTopMainedit6.Left = 350
PetOnTopMainedit6.Width = 40
PetOnTopMainedit7=createEdit(PetModelForm)
PetOnTopMainedit7.Top = 350
PetOnTopMainedit7.Left = 350
PetOnTopMainedit7.Width = 40
PetOnTopMainedit8=createEdit(PetModelForm)
PetOnTopMainedit8.Top = 400
PetOnTopMainedit8.Left = 350
PetOnTopMainedit8.Width = 40
PetOnTopMainedit.Visible = false
PetOnTopMainedit2.Visible = false
PetOnTopMainedit3.Visible = false
PetOnTopMainedit4.Visible = false
PetOnTopMainedit5.Visible = false
PetOnTopMainedit6.Visible = false
PetOnTopMainedit7.Visible = false
PetOnTopMainedit8.Visible = false
PetOnTopBSedit=createEdit(PetModelForm)
PetOnTopBSedit.Top = 50
PetOnTopBSedit.Left = 350
PetOnTopBSedit.Width = 40
PetOnTopBSedit2=createEdit(PetModelForm)
PetOnTopBSedit2.Top = 100
PetOnTopBSedit2.Left = 350
PetOnTopBSedit2.Width = 40
PetOnTopBSedit3=createEdit(PetModelForm)
PetOnTopBSedit3.Top = 150
PetOnTopBSedit3.Left = 350
PetOnTopBSedit3.Width = 40
PetOnTopBSedit4=createEdit(PetModelForm)
PetOnTopBSedit4.Top = 200
PetOnTopBSedit4.Left = 350
PetOnTopBSedit4.Width = 40
PetOnTopBSedit5=createEdit(PetModelForm)
PetOnTopBSedit5.Top = 250
PetOnTopBSedit5.Left = 350
PetOnTopBSedit5.Width = 40
PetOnTopBSedit6=createEdit(PetModelForm)
PetOnTopBSedit6.Top = 300
PetOnTopBSedit6.Left = 350
PetOnTopBSedit6.Width = 40
PetOnTopBSedit7=createEdit(PetModelForm)
PetOnTopBSedit7.Top = 350
PetOnTopBSedit7.Left = 350
PetOnTopBSedit7.Width = 40
PetOnTopBSedit8=createEdit(PetModelForm)
PetOnTopBSedit8.Top = 400
PetOnTopBSedit8.Left = 350
PetOnTopBSedit8.Width = 40
PetOnTopBSedit.Visible = false
PetOnTopBSedit2.Visible = false
PetOnTopBSedit3.Visible = false
PetOnTopBSedit4.Visible = false
PetOnTopBSedit5.Visible = false
PetOnTopBSedit6.Visible = false
PetOnTopBSedit7.Visible = false
PetOnTopBSedit8.Visible = false
PetOnTopBRedit2=createEdit(PetModelForm)
PetOnTopBRedit2.Top = 100
PetOnTopBRedit2.Left = 350
PetOnTopBRedit2.Width = 40
PetOnTopBRedit3=createEdit(PetModelForm)
PetOnTopBRedit3.Top = 150
PetOnTopBRedit3.Left = 350
PetOnTopBRedit3.Width = 40
PetOnTopBRedit4=createEdit(PetModelForm)
PetOnTopBRedit4.Top = 200
PetOnTopBRedit4.Left = 350
PetOnTopBRedit4.Width = 40
PetOnTopBRedit5=createEdit(PetModelForm)
PetOnTopBRedit5.Top = 250
PetOnTopBRedit5.Left = 350
PetOnTopBRedit5.Width = 40
PetOnTopBRedit6=createEdit(PetModelForm)
PetOnTopBRedit6.Top = 300
PetOnTopBRedit6.Left = 350
PetOnTopBRedit6.Width = 40
PetOnTopBRedit7=createEdit(PetModelForm)
PetOnTopBRedit7.Top = 350
PetOnTopBRedit7.Left = 350
PetOnTopBRedit7.Width = 40
PetOnTopBRedit8=createEdit(PetModelForm)
PetOnTopBRedit8.Top = 400
PetOnTopBRedit8.Left = 350
PetOnTopBRedit8.Width = 40
PetOnTopBRedit2.Visible = false
PetOnTopBRedit3.Visible = false
PetOnTopBRedit4.Visible = false
PetOnTopBRedit5.Visible = false
PetOnTopBRedit6.Visible = false
PetOnTopBRedit7.Visible = false
PetOnTopBRedit8.Visible = false
PetOnTopBPeditX2=createEdit(PetModelForm)
PetOnTopBPeditX2.Top = 50
PetOnTopBPeditX2.Left = 50
PetOnTopBPeditX2.Width = 45
PetOnTopBPeditX3=createEdit(PetModelForm)
PetOnTopBPeditX3.Top = 120
PetOnTopBPeditX3.Left = 50
PetOnTopBPeditX3.Width = 45
PetOnTopBPeditX4=createEdit(PetModelForm)
PetOnTopBPeditX4.Top = 190
PetOnTopBPeditX4.Left = 50
PetOnTopBPeditX4.Width = 45
PetOnTopBPeditX5=createEdit(PetModelForm)
PetOnTopBPeditX5.Top = 260
PetOnTopBPeditX5.Left = 50
PetOnTopBPeditX5.Width = 45
PetOnTopBPeditX6=createEdit(PetModelForm)
PetOnTopBPeditX6.Top = 330
PetOnTopBPeditX6.Left = 50
PetOnTopBPeditX6.Width = 45
PetOnTopBPeditX7=createEdit(PetModelForm)
PetOnTopBPeditX7.Top = 400
PetOnTopBPeditX7.Left = 50
PetOnTopBPeditX7.Width = 45
PetOnTopBPeditY2=createEdit(PetModelForm)
PetOnTopBPeditY2.Top = 50
PetOnTopBPeditY2.Left = 180
PetOnTopBPeditY2.Width = 45
PetOnTopBPeditY3=createEdit(PetModelForm)
PetOnTopBPeditY3.Top = 120
PetOnTopBPeditY3.Left = 180
PetOnTopBPeditY3.Width = 45
PetOnTopBPeditY4=createEdit(PetModelForm)
PetOnTopBPeditY4.Top = 190
PetOnTopBPeditY4.Left = 180
PetOnTopBPeditY4.Width = 45
PetOnTopBPeditY5=createEdit(PetModelForm)
PetOnTopBPeditY5.Top = 260
PetOnTopBPeditY5.Left = 180
PetOnTopBPeditY5.Width = 45
PetOnTopBPeditY6=createEdit(PetModelForm)
PetOnTopBPeditY6.Top = 330
PetOnTopBPeditY6.Left = 180
PetOnTopBPeditY6.Width = 45
PetOnTopBPeditY7=createEdit(PetModelForm)
PetOnTopBPeditY7.Top = 400
PetOnTopBPeditY7.Left = 180
PetOnTopBPeditY7.Width = 45
PetOnTopBPeditZ2=createEdit(PetModelForm)
PetOnTopBPeditZ2.Top = 50
PetOnTopBPeditZ2.Left = 310
PetOnTopBPeditZ2.Width = 45
PetOnTopBPeditZ3=createEdit(PetModelForm)
PetOnTopBPeditZ3.Top = 120
PetOnTopBPeditZ3.Left = 310
PetOnTopBPeditZ3.Width = 45
PetOnTopBPeditZ4=createEdit(PetModelForm)
PetOnTopBPeditZ4.Top = 190
PetOnTopBPeditZ4.Left = 310
PetOnTopBPeditZ4.Width = 45
PetOnTopBPeditZ4.Height = 15
PetOnTopBPeditZ5=createEdit(PetModelForm)
PetOnTopBPeditZ5.Top = 260
PetOnTopBPeditZ5.Left = 310
PetOnTopBPeditZ5.Width = 45
PetOnTopBPeditZ6=createEdit(PetModelForm)
PetOnTopBPeditZ6.Top = 330
PetOnTopBPeditZ6.Left = 310
PetOnTopBPeditZ6.Width = 45
PetOnTopBPeditZ7=createEdit(PetModelForm)
PetOnTopBPeditZ7.Top = 400
PetOnTopBPeditZ7.Left = 310
PetOnTopBPeditZ7.Width = 45
PetOnTopBPeditX2.Visible = false
PetOnTopBPeditX3.Visible = false
PetOnTopBPeditX4.Visible = false
PetOnTopBPeditX5.Visible = false
PetOnTopBPeditX6.Visible = false
PetOnTopBPeditX7.Visible = false
PetOnTopBPeditY2.Visible = false
PetOnTopBPeditY3.Visible = false
PetOnTopBPeditY4.Visible = false
PetOnTopBPeditY5.Visible = false
PetOnTopBPeditY6.Visible = false
PetOnTopBPeditY7.Visible = false
PetOnTopBPeditZ2.Visible = false
PetOnTopBPeditZ3.Visible = false
PetOnTopBPeditZ4.Visible = false
PetOnTopBPeditZ5.Visible = false
PetOnTopBPeditZ6.Visible = false
PetOnTopBPeditZ7.Visible = false
PetOnTopHBedit=createEdit(PetModelForm)
PetOnTopHBedit.Top = 175
PetOnTopHBedit.Left = 180
PetOnTopHBedit.Width = 35
PetOnTopHBedit2=createEdit(PetModelForm)
PetOnTopHBedit2.Top = 275
PetOnTopHBedit2.Left = 180
PetOnTopHBedit2.Width = 35
PetOnTopHBedit3=createEdit(PetModelForm)
PetOnTopHBedit3.Top = 375
PetOnTopHBedit3.Left = 180
PetOnTopHBedit3.Width = 35
PetOnTopHBedit.Visible = false
PetOnTopHBedit2.Visible = false
PetOnTopHBedit3.Visible = false
PetSetOnTopEdit = createButton(PetModelForm)
PetSetOnTopEdit.Caption = 'Set'
PetSetOnTopEdit.Top = 435
PetSetOnTopEdit.Left = 350
PetSetOnTopEdit.Width = 40
setMethodProperty(PetOnTopMainedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopMainedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBSedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBRedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditX7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditY7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopBPeditZ7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopHBedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopHBedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(PetOnTopHBedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)

--TestValueSendOnEditBox
PetSetOnTopEdit.OnClick = function (sender)
  setProperty(PetOnTopMainedit, 'text', Petslider.Position)
  setProperty(PetOnTopMainedit2, 'text', Petslider2.Position)
  setProperty(PetOnTopMainedit3, 'text', Petslider3.Position)
  setProperty(PetOnTopMainedit4, 'text', Petslider4.Position)
  setProperty(PetOnTopMainedit5, 'text', Petslider5.Position)
  setProperty(PetOnTopMainedit6, 'text', Petslider6.Position)
  setProperty(PetOnTopMainedit7, 'text', Petslider7.Position)
  setProperty(PetOnTopMainedit8, 'text', Petslider8.Position)
  setProperty(PetOnTopBSedit, 'text', PetsliderBS.Position*0.01)
  setProperty(PetOnTopBSedit2, 'text', PetsliderBS2.Position*0.01)
  setProperty(PetOnTopBSedit3, 'text', PetsliderBS3.Position*0.01)
  setProperty(PetOnTopBSedit4, 'text', PetsliderBS4.Position*0.01)
  setProperty(PetOnTopBSedit5, 'text', PetsliderBS5.Position*0.01)
  setProperty(PetOnTopBSedit6, 'text', PetsliderBS6.Position*0.01)
  setProperty(PetOnTopBSedit7, 'text', PetsliderBS7.Position*0.01)
  setProperty(PetOnTopBSedit8, 'text', PetsliderBS8.Position*0.01)
  setProperty(PetOnTopBRedit2, 'text', PetsliderBR2.Position)
  setProperty(PetOnTopBRedit3, 'text', PetsliderBR3.Position)
  setProperty(PetOnTopBRedit4, 'text', PetsliderBR4.Position)
  setProperty(PetOnTopBRedit5, 'text', PetsliderBR5.Position)
  setProperty(PetOnTopBRedit6, 'text', PetsliderBR6.Position)
  setProperty(PetOnTopBRedit7, 'text', PetsliderBR7.Position)
  setProperty(PetOnTopBRedit8, 'text', PetsliderBR8.Position)
  setProperty(PetOnTopBPeditX2, 'text', PetsliderBPX.Position)
  setProperty(PetOnTopBPeditX3, 'text', PetsliderBPX2.Position)
  setProperty(PetOnTopBPeditX4, 'text', PetsliderBPX3.Position)
  setProperty(PetOnTopBPeditX5, 'text', PetsliderBPX4.Position)
  setProperty(PetOnTopBPeditX6, 'text', PetsliderBPX5.Position)
  setProperty(PetOnTopBPeditX7, 'text', PetsliderBPX6.Position)
  setProperty(PetOnTopBPeditY2, 'text', PetsliderBPY1.Position)
  setProperty(PetOnTopBPeditY3, 'text', PetsliderBPY2.Position)
  setProperty(PetOnTopBPeditY4, 'text', PetsliderBPY3.Position)
  setProperty(PetOnTopBPeditY5, 'text', PetsliderBPY4.Position)
  setProperty(PetOnTopBPeditY6, 'text', PetsliderBPY5.Position)
  setProperty(PetOnTopBPeditY7, 'text', PetsliderBPY6.Position)
  setProperty(PetOnTopBPeditZ2, 'text', PetsliderBPZ1.Position)
  setProperty(PetOnTopBPeditZ3, 'text', PetsliderBPZ2.Position)
  setProperty(PetOnTopBPeditZ4, 'text', PetsliderBPZ3.Position)
  setProperty(PetOnTopBPeditZ5, 'text', PetsliderBPZ4.Position)
  setProperty(PetOnTopBPeditZ6, 'text', PetsliderBPZ5.Position)
  setProperty(PetOnTopBPeditZ7, 'text', PetsliderBPZ6.Position)
  setProperty(PetOnTopHBedit, 'text', PetsliderHB.Position*0.01)
  setProperty(PetOnTopHBedit2, 'text', PetsliderHB2.Position*0.01)
  setProperty(PetOnTopHBedit3, 'text', PetsliderHB3.Position*0.01)

 if(checkbox_getState(Pettoggle) == 1) and PetOnTopMainedit.visible == true then
PetOnTopMainedit.Visible = false
PetOnTopMainedit2.Visible = false
PetOnTopMainedit3.Visible = false
PetOnTopMainedit4.Visible = false
PetOnTopMainedit5.Visible = false
PetOnTopMainedit6.Visible = false
PetOnTopMainedit7.Visible = false
PetOnTopMainedit8.Visible = false
setProperty(Petslider, 'Position', getProperty(PetOnTopMainedit, 'text'))
setProperty(Petslider2, 'Position', getProperty(PetOnTopMainedit2, 'text'))
setProperty(Petslider3, 'Position', getProperty(PetOnTopMainedit3, 'text'))
setProperty(Petslider4, 'Position', getProperty(PetOnTopMainedit4, 'text'))
setProperty(Petslider5, 'Position', getProperty(PetOnTopMainedit5, 'text'))
setProperty(Petslider6, 'Position', getProperty(PetOnTopMainedit6, 'text'))
setProperty(Petslider7, 'Position', getProperty(PetOnTopMainedit7, 'text'))
setProperty(Petslider8, 'Position', getProperty(PetOnTopMainedit8, 'text'))
 elseif(checkbox_getState(PettoggleBS) == 1) and PetOnTopBSedit.visible == true then
PetOnTopBSedit.Visible = false
PetOnTopBSedit2.Visible = false
PetOnTopBSedit3.Visible = false
PetOnTopBSedit4.Visible = false
PetOnTopBSedit5.Visible = false
PetOnTopBSedit6.Visible = false
PetOnTopBSedit7.Visible = false
PetOnTopBSedit8.Visible = false
setProperty(PetsliderBS, 'Position', (round(tonumber(getProperty(PetOnTopBSedit, 'text')/0.01))))
setProperty(PetsliderBS2, 'Position',(round(tonumber(getProperty(PetOnTopBSedit2, 'text')/0.01))))
setProperty(PetsliderBS3, 'Position',(round(tonumber(getProperty(PetOnTopBSedit3, 'text')/0.01))))
setProperty(PetsliderBS4, 'Position',(round(tonumber(getProperty(PetOnTopBSedit4, 'text')/0.01))))
setProperty(PetsliderBS5, 'Position',(round(tonumber(getProperty(PetOnTopBSedit5, 'text')/0.01))))
setProperty(PetsliderBS6, 'Position',(round(tonumber(getProperty(PetOnTopBSedit6, 'text')/0.01))))
setProperty(PetsliderBS7, 'Position',(round(tonumber(getProperty(PetOnTopBSedit7, 'text')/0.01))))
setProperty(PetsliderBS8, 'Position',(round(tonumber(getProperty(PetOnTopBSedit8, 'text')/0.01))))
 elseif(checkbox_getState(PettoggleBR) == 1) and PetOnTopBRedit2.visible == true then
PetOnTopBRedit2.Visible = false
PetOnTopBRedit3.Visible = false
PetOnTopBRedit4.Visible = false
PetOnTopBRedit5.Visible = false
PetOnTopBRedit6.Visible = false
PetOnTopBRedit7.Visible = false
PetOnTopBRedit8.Visible = false
setProperty(PetsliderBR2, 'Position', getProperty(PetOnTopBRedit2, 'text'))
setProperty(PetsliderBR3, 'Position', getProperty(PetOnTopBRedit3, 'text'))
setProperty(PetsliderBR4, 'Position', getProperty(PetOnTopBRedit4, 'text'))
setProperty(PetsliderBR5, 'Position', getProperty(PetOnTopBRedit5, 'text'))
setProperty(PetsliderBR6, 'Position', getProperty(PetOnTopBRedit6, 'text'))
setProperty(PetsliderBR7, 'Position', getProperty(PetOnTopBRedit7, 'text'))
setProperty(PetsliderBR8, 'Position', getProperty(PetOnTopBRedit8, 'text'))
 elseif(checkbox_getState(PettoggleBP) == 1) and PetOnTopBPeditX2.visible == true then
PetOnTopBPeditX2.Visible = false
PetOnTopBPeditX3.Visible = false
PetOnTopBPeditX4.Visible = false
PetOnTopBPeditX5.Visible = false
PetOnTopBPeditX6.Visible = false
PetOnTopBPeditX7.Visible = false
setProperty(PetsliderBPX, 'Position', getProperty(PetOnTopBPeditX2, 'text'))
setProperty(PetsliderBPX2, 'Position', getProperty(PetOnTopBPeditX3, 'text'))
setProperty(PetsliderBPX3, 'Position', getProperty(PetOnTopBPeditX4, 'text'))
setProperty(PetsliderBPX4, 'Position', getProperty(PetOnTopBPeditX5, 'text'))
setProperty(PetsliderBPX5, 'Position', getProperty(PetOnTopBPeditX6, 'text'))
setProperty(PetsliderBPX6, 'Position', getProperty(PetOnTopBPeditX7, 'text'))
PetOnTopBPeditY2.Visible = false
PetOnTopBPeditY3.Visible = false
PetOnTopBPeditY4.Visible = false
PetOnTopBPeditY5.Visible = false
PetOnTopBPeditY6.Visible = false
PetOnTopBPeditY7.Visible = false
setProperty(PetsliderBPY1, 'Position', getProperty(PetOnTopBPeditY2, 'text'))
setProperty(PetsliderBPY2, 'Position', getProperty(PetOnTopBPeditY3, 'text'))
setProperty(PetsliderBPY3, 'Position', getProperty(PetOnTopBPeditY4, 'text'))
setProperty(PetsliderBPY4, 'Position', getProperty(PetOnTopBPeditY5, 'text'))
setProperty(PetsliderBPY5, 'Position', getProperty(PetOnTopBPeditY6, 'text'))
setProperty(PetsliderBPY6, 'Position', getProperty(PetOnTopBPeditY7, 'text'))
PetOnTopBPeditZ2.Visible = false
PetOnTopBPeditZ3.Visible = false
PetOnTopBPeditZ4.Visible = false
PetOnTopBPeditZ5.Visible = false
PetOnTopBPeditZ6.Visible = false
PetOnTopBPeditZ7.Visible = false
setProperty(PetsliderBPZ1, 'Position', getProperty(PetOnTopBPeditZ2, 'text'))
setProperty(PetsliderBPZ2, 'Position', getProperty(PetOnTopBPeditZ3, 'text'))
setProperty(PetsliderBPZ3, 'Position', getProperty(PetOnTopBPeditZ4, 'text'))
setProperty(PetsliderBPZ4, 'Position', getProperty(PetOnTopBPeditZ5, 'text'))
setProperty(PetsliderBPZ5, 'Position', getProperty(PetOnTopBPeditZ6, 'text'))
setProperty(PetsliderBPZ6, 'Position', getProperty(PetOnTopBPeditZ7, 'text'))
 elseif(checkbox_getState(PettoggleHB) == 1) and PetOnTopHBedit.visible == true then
PetOnTopHBedit.Visible = false
PetOnTopHBedit2.Visible = false
PetOnTopHBedit3.Visible = false
setProperty(PetsliderHB, 'Position', (round(tonumber(getProperty(PetOnTopHBedit, 'text')/0.01))))
setProperty(PetsliderHB2, 'Position',(round(tonumber(getProperty(PetOnTopHBedit2, 'text')/0.01))))
setProperty(PetsliderHB3, 'Position',(round(tonumber(getProperty(PetOnTopHBedit3, 'text')/0.01))))


 elseif(checkbox_getState(Pettoggle) == 1) and PetOnTopMainedit.visible == false then
PetOnTopMainedit.Visible = true
PetOnTopMainedit2.Visible = true
PetOnTopMainedit3.Visible = true
PetOnTopMainedit4.Visible = true
PetOnTopMainedit5.Visible = true
PetOnTopMainedit6.Visible = true
PetOnTopMainedit7.Visible = true
PetOnTopMainedit8.Visible = true
 elseif(checkbox_getState(PettoggleBS) == 1) and PetOnTopBSedit.visible == false then
PetOnTopBSedit.Visible = true
PetOnTopBSedit2.Visible = true
PetOnTopBSedit3.Visible = true
PetOnTopBSedit4.Visible = true
PetOnTopBSedit5.Visible = true
PetOnTopBSedit6.Visible = true
PetOnTopBSedit7.Visible = true
PetOnTopBSedit8.Visible = true
 elseif(checkbox_getState(PettoggleBR) == 1) and PetOnTopBRedit2.visible == false then
PetOnTopBRedit2.Visible = true
PetOnTopBRedit3.Visible = true
PetOnTopBRedit4.Visible = true
PetOnTopBRedit5.Visible = true
PetOnTopBRedit6.Visible = true
PetOnTopBRedit7.Visible = true
PetOnTopBRedit8.Visible = true
 elseif(checkbox_getState(PettoggleBP) == 1) and PetOnTopBPeditX2.visible == false then
PetOnTopBPeditX2.Visible = true
PetOnTopBPeditX3.Visible = true
PetOnTopBPeditX4.Visible = true
PetOnTopBPeditX5.Visible = true
PetOnTopBPeditX6.Visible = true
PetOnTopBPeditX7.Visible = true
PetOnTopBPeditY2.Visible = true
PetOnTopBPeditY3.Visible = true
PetOnTopBPeditY4.Visible = true
PetOnTopBPeditY5.Visible = true
PetOnTopBPeditY6.Visible = true
PetOnTopBPeditY7.Visible = true
PetOnTopBPeditZ2.Visible = true
PetOnTopBPeditZ3.Visible = true
PetOnTopBPeditZ4.Visible = true
PetOnTopBPeditZ5.Visible = true
PetOnTopBPeditZ6.Visible = true
PetOnTopBPeditZ7.Visible = true
 elseif(checkbox_getState(PettoggleHB) == 1) and PetOnTopHBedit.visible == false then
PetOnTopHBedit.Visible = true
PetOnTopHBedit2.Visible = true
PetOnTopHBedit3.Visible = true
end
end



--SpritesTestForm
local spritesTestForm = createForm(false)
spritesTestForm.Caption='Sprites'
spritesTestForm.Height = 400
spritesTestForm.Width = 600
spritesTestForm.Top = 380
spritesTestForm.Left = 200
spritesTestForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox3, 0)
   return caHide
end
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(spritesTestForm, [[SpritesForm.png]])
cbWeapSelector = createComboBox(spritesTestForm)
cbWeapSelector.Width = 125
cbWeapSelector.top = 10
cbWeapSelector.left = 250
cbWeapSelectoritem = cbWeapSelector.getItems
cbWeapSelector.style = 'csDropDownList'
cbWeapSelector.items.add("WeaponToReplace")
cbWeapSelector.items.add("Dagger")
cbWeapSelector.items.add("Bow")
cbWeapSelector.items.add("Crossbow")
cbWeapSelector.items.add("Shield")
cbWeapSelector.items.add("Sword")
cbWeapSelector.items.add("Longsword")
cbWeapSelector.items.add("Fist")
cbWeapSelector.items.add("Wand")
cbWeapSelector.Visible = false
setProperty(cbWeapSelector, "ItemIndex", "0")
cbRaceSelector = createComboBox(spritesTestForm)
cbRaceSelector.Width = 125
cbRaceSelector.top = 10
cbRaceSelector.left = 250
cbRaceSelectoritem = cbRaceSelector.getItems
cbRaceSelector.style = 'csDropDownList'
cbRaceSelector.items.add("RaceToReplace")
cbRaceSelector.items.add("Human")
cbRaceSelector.items.add("Elf")
cbRaceSelector.items.add("Dwarf")
cbRaceSelector.items.add("Orc")
cbRaceSelector.items.add("Goblin")
cbRaceSelector.items.add("Lizard")
cbRaceSelector.items.add("Undead")
cbRaceSelector.items.add("Frogman")
cbRaceSelector.Visible = false
setProperty(cbRaceSelector, "ItemIndex", "0")
cbSpritesSelector = createComboBox(spritesTestForm)
cbSpritesSelector.Width = 200
cbSpritesSelector.top = 10
cbSpritesSelector.left = 10
cbSpritesSelectoritem = cbSpritesSelector.getItems
cbSpritesSelector.style = 'csDropDownList'
cbSpritesSelector.items.add("SpritesSelector")
cbSpritesSelector.items.add("Glider")
cbSpritesSelector.items.add("Boat")
cbSpritesSelector.items.add("Lantern")
cbSpritesSelector.items.add("Race")
cbSpritesSelector.items.add("Weapon")
setProperty(cbSpritesSelector, "ItemIndex", "0")
LabelBasicGlider=createLabel(spritesTestForm)
LabelBasicGlider.setCaption('Change To ->')
LabelBasicGlider.Font.Color = 0xffffff
LabelBasicGlider.Font.Size = 12
LabelBasicGlider.Font.Style = ('fsUnderline, fsBold')
LabelBasicGlider.Top = 100
LabelBasicGlider.Left = 250
LabelBasicGlider.Visible = false
ReplaceButton=createButton(spritesTestForm)
ReplaceButton.top = 350
ReplaceButton.Caption = 'Replace .Cub'
ReplaceButton.Width = 100
ReplaceButton.Height = 25
ReplaceButton.left = 490
GliderCB=createComboBox(spritesTestForm)
GliderCB.Width = 150
GliderCB.top = 100
GliderCB.left = 50
GliderCBitem = GliderCB.getItems
GliderCB.style = 'csDropDownList'
GliderCB.items.add("glider.Cub")
GliderCBReplace=createComboBox(spritesTestForm)
GliderCBReplace.Width = 150
GliderCBReplace.top = 100
GliderCBReplace.left = 400
GliderCBReplaceitem = GliderCBReplace.getItems
GliderCBReplace.style = 'csDropDownList'
GliderCBReplace.items.add("Glider(rustic).Cub")
cbSpritesSelector.Onchange = function(sender)
 if cbSpritesSelector.ItemIndex == 0 then
  cbRaceSelector.Visible = false
  cbWeapSelector.Visible = false
  LabelBasicGlider.Visible = false
 elseif cbSpritesSelector.ItemIndex == 1 then
  cbRaceSelector.Visible = false
  cbWeapSelector.Visible = false
  LabelBasicGlider.Visible = true
 elseif cbSpritesSelector.ItemIndex == 2 then
  cbRaceSelector.Visible = false
  cbWeapSelector.Visible = false
  LabelBasicGlider.Visible = true
 elseif cbSpritesSelector.ItemIndex == 3 then
  cbRaceSelector.Visible = false
  cbWeapSelector.Visible = false
  LabelBasicGlider.Visible = true
 elseif cbSpritesSelector.ItemIndex == 4 then
 cbRaceSelector.Visible = true
 cbWeapSelector.Visible = false
 elseif cbSpritesSelector.ItemIndex == 5 then
 cbWeapSelector.Visible = true
 cbRaceSelector.Visible = false
 end
end
--SpritesSwapToggleButton OnMainForm
function UDF1_CEToggleBox3Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox3) == 1) then
spritesTestForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox3) == 0) then
spritesTestForm.hide()
  end
end

--CharCreationTestForm
CCForm = createForm(false)
CCForm.Caption='CharacterCreationTweak'
CCForm.Height = 500
CCForm.Width = 325
CCForm.Top = 380
CCForm.Left = 325
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(CCForm, [[CharacterCreation.png]])
CCcheckBox = createCheckBox(CCForm)
CCcheckBox.Top = 10
CCcheckBox.Left = 15
CCcheckBoxLabel = createLabel(CCForm)
CCcheckBoxLabel.Top = 10
CCcheckBoxLabel.Left = 30
CCcheckBoxLabel.setCaption('Character Creation Menu')
CCcheckBoxLabel.Font.Color = 0xffffff
CCcheckBoxLabel.Font.Style = ('fsUnderline, fsBold')
CCcheckBox.OnChange = function(sender)
   if(checkbox_getState(CCcheckBox) == 1) then
   writeInteger('[[[[cubeworld.exe+00551E80]+120]+68]+E0]+0', 1)
   elseif (checkbox_getState(CCcheckBox) == 0) then
   writeInteger('[[[[cubeworld.exe+00551E80]+120]+68]+E0]+0', 0)
end
end
CCNameButton=createToggleBox(CCForm)
CCNameButton.Top = 63
CCNameButton.Left = 248
CCNameButton.Width = 50
CCNameButton.Caption = 'Change'
CCNameButton.OnChange = function (sender)
 if(checkbox_getState(CCNameButton) == 0) then
  writeString('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+958', CCNameEditOnTop.Text)
  CCNameEditOnTop.Visible=false
 elseif(checkbox_getState(CCNameButton) == 1) then
  CCNameEditOnTop.Visible=true
 end
end
CCNameEdit=createEdit(CCForm)
CCNameEdit.Top = 63
CCNameEdit.Left = 30
CCNameEdit.Width = 217
CCNameEdit.Font.Size = 10
CCNameEditRefreshTimer = createTimer(getMainForm())
CCNameEditRefreshTimer.Interval = 100
CCNameEditRefreshTimer.onTimer = function(sender)
  if CCNameEdit.text == readString('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+958', 25) then
  else
  setProperty(CCNameEdit, 'text', readString('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+958', 25))
 end
end
CCNameEditOnTop=createEdit(CCForm)
CCNameEditOnTop.Top = 63
CCNameEditOnTop.Left = 30
CCNameEditOnTop.Width = 217
CCNameEditOnTop.Font.Size = 10
CCNameEditOnTop.Visible = false
CCRaceLabel=createLabel(CCForm)
CCRaceLabel.Top = 125
CCRaceLabel.Left = 140
CCRaceLabel.setCaption('Race')
CCRaceLabel.Font.Color = 0xffffff
CCRaceLabel.Font.Style = ('fsUnderline, fsBold')
CCRaceLabel.Font.Size = 13
EditBoxRaceTracker = createEdit(CCForm)
EditBoxRaceTracker.Top = 125
EditBoxRaceTracker.Left = 125
EditBoxRaceTracker.visible = false
EditBoxRefreshTimer = createTimer(getMainForm())
EditBoxRefreshTimer.Interval = 100
EditBoxRefreshTimer.onTimer = function(sender)
  if EditBoxRaceTracker.text == CCraceBar.position then
  else
  setProperty(EditBoxRaceTracker, 'text', CCraceBar.position)
 end
end
CCraceBarComboBox=createComboBox(CCForm)
CCraceBarComboBox.Top=180
CCraceBarComboBox.Left=110
CCraceBarComboBoxitem = CCraceBarComboBox.getItems
CCraceBarComboBox.style = 'csDropDownList'
CCraceBarComboBox.items.add(" ")
CCraceBarComboBox.items.add("Ogre")
CCraceBarComboBox.items.add("Cyclops")
CCraceBarComboBox.items.add("Pachyderm")
CCraceBarComboBox.items.add("LavaMan")
CCraceBarComboBox.items.add("Witch")
CCraceBarComboBox.items.add("SpikeMan")
CCraceBarComboBox.items.add("Koala")
CCraceBarComboBox.items.add("Spectrino")
CCraceBarComboBox.items.add("BlueCrab")
CCraceBarComboBox.items.add("Penguin")
CCraceBarComboBox.items.add("DarkJester")
CCraceBarComboBox.items.add("Jester")
CCraceBarComboBox.items.add("Insectoid")
CCraceBarComboBox.items.add("Insectoid2")
CCraceBarComboBox.items.add("Mermaid")
CCraceBarComboBox.items.add("Merman")
CCraceBarComboBox.items.add("BlueGnome")
CCraceBarComboBox.items.add("GreenGnome")
CCraceBarComboBox.items.add("Gnoll")
CCraceBarComboBox.items.add("OldMan")
CCraceBarComboBox.items.add("PolarGnobolt")
CCraceBarComboBox.items.add("Test")
CCraceBarComboBox.items.add("Test")
CCraceBarComboBox.items.add("Test")
setProperty(CCraceBarComboBox, "ItemIndex", "0")
--ComboBoxRaceFromTrackBarPosition
CCraceBarComboBox.OnChange=function(sender)
 setProperty(CCraceBar, 'position', CCraceBarComboBox.ItemIndex)
end
CCraceBar= createTrackBar(CCForm)
CCraceBar.Top = 150
CCraceBar.Left = 10
CCraceBar.Min = 0
CCraceBar.Max = 50
CCraceBar.Width = 300
CCraceBar.OnChange= function (sender)
 setProperty(CCraceBarComboBox, 'ItemIndex',CCraceBar.position)
--FonctionForNil--Test Could Possibly delete the timer and all
 if CCraceBar.position == 0 then
ourValue = nil
freezeTimer0 = createTimer(getMainForm())
freezeTimer0.Interval = 1000
freezeTimer0.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 0 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer0.destroy()
   end
 end
end
--FonctionForOgre
 if CCraceBar.position == 1 then
ourValue = nil
freezeTimer1 = createTimer(getMainForm())
freezeTimer1.Interval = 1000
freezeTimer1.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 1 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",81)--Head
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",82)--Body
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",83)--Hand
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",84)--Feet
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer1.destroy()
   end
 end
end
--FonctionForCyclops
 if CCraceBar.position ==2 then
ourValue = nil
freezeTimer2 = createTimer(getMainForm())
freezeTimer2.Interval = 1000
freezeTimer2.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 2 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",88)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",89)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",90)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",91)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer2.destroy()
   end
 end
end
--FonctionForPachyderm
 if CCraceBar.position ==3 then
ourValue = nil
freezeTimer3 = createTimer(getMainForm())
freezeTimer3.Interval = 1000
freezeTimer3.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 3 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",96)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",97)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",86)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",98)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue;
      freezeTimer3.destroy()
   end
 end
end
--FonctionForLavaMan
 if CCraceBar.position ==4 then
ourValue = nil
freezeTimer4 = createTimer(getMainForm())
freezeTimer4.Interval = 1000
freezeTimer4.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 4 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",66)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",67)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",68)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",69)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer4.destroy()
   end
 end
end
--FonctionForWitch
 if CCraceBar.position ==5 then
ourValue = nil
freezeTimer5 = createTimer(getMainForm())
freezeTimer5.Interval = 1000
freezeTimer5.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 5 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",16)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",17)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",18)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",615)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer5.destroy()
   end
 end
end
--FonctionForSpikeMen
 if CCraceBar.position ==6 then
ourValue = nil
freezeTimer6 = createTimer(getMainForm())
freezeTimer6.Interval = 1000
freezeTimer6.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 6 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",256)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",258)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",187)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",257)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer6.destroy()
   end
 end
end
--FonctionForKoala
 if CCraceBar.position ==7 then
ourValue = nil
freezeTimer7 = createTimer(getMainForm())
freezeTimer7.Interval = 1000
freezeTimer7.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 7 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",236)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",235)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",238)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",237)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer7.destroy()
   end
 end
end
--FonctionForSpectrino
 if CCraceBar.position ==8 then
ourValue = nil
freezeTimer8 = createTimer(getMainForm())
freezeTimer8.Interval = 1000
freezeTimer8.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 8 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",276)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",278)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",279)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",277)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer8.destroy()
   end
 end
end
--FonctionForBlueCrab
 if CCraceBar.position ==9 then
ourValue = nil
freezeTimer9 = createTimer(getMainForm())
freezeTimer9.Interval = 1000
freezeTimer9.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 9 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",326)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",325)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",328)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",327)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer9.destroy()
   end
 end
end
--FonctionForPenguin
 if CCraceBar.position ==10 then
ourValue = nil
freezeTimer10 = createTimer(getMainForm())
freezeTimer10.Interval = 1000
freezeTimer10.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   if CCraceBar.position == 10 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",318)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",317)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",320)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",319)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer10.destroy()
   end
 end
end
--FonctionForDarkJester
 if CCraceBar.position ==11 then
ourValue = nil
freezeTimer11 = createTimer(getMainForm())
freezeTimer11.Interval = 1000
freezeTimer11.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==11 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",272)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",274)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",275)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",273)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer11.destroy()
 end
 end
end
--FonctionForNormalJester
if CCraceBar.position ==12 then
ourValue = nil
freezeTimer12 = createTimer(getMainForm())
freezeTimer12.Interval = 1000
freezeTimer12.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==12 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",268)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",270)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",271)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",269)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer12.destroy()
 end
 end
end
--FonctionForInsectoid
if CCraceBar.position ==13 then
ourValue = nil
freezeTimer13 = createTimer(getMainForm())
freezeTimer13.Interval = 1000
freezeTimer13.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==13 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",3256)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",3258)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",3257)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",3255)
--ProblyNotUsefullSinceNpcModel--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer13.destroy()
 end
 end
end
--FonctionForInsectoid2
if CCraceBar.position ==14 then
ourValue = nil
freezeTimer14 = createTimer(getMainForm())
freezeTimer14.Interval = 1000
freezeTimer14.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==14 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",3260)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",3262)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",3261)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",3259)
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer14.destroy()
 end
 end
end
--FonctionForMermaid
if CCraceBar.position ==15 then
ourValue = nil
freezeTimer15 = createTimer(getMainForm())
freezeTimer15.Interval = 1000
freezeTimer15.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==15 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",1556)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",1562)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",1563)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",-1)--noFeet
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92",1560)--HairRemoveOnceHairTracker
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer15.destroy()
 end
 end
end
--FonctionForMerman
if CCraceBar.position ==16 then
ourValue = nil
freezeTimer16 = createTimer(getMainForm())
freezeTimer16.Interval = 1000
freezeTimer16.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==16 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",1565)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",1570)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",1563)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",-1)--noFeet
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92",1569)--Hair
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer16.destroy()
 end
 end
end
--FonctionForBlueGnome
if CCraceBar.position ==17 then
ourValue = nil
freezeTimer17 = createTimer(getMainForm())
freezeTimer17.Interval = 1000
freezeTimer17.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==17 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",3643)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",1)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",613)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",615)
--ProblyNotUsefullSinceNpcModel--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer17.destroy()
 end
 end
end
--FonctionForGreenGnome
if CCraceBar.position ==18 then
ourValue = nil
freezeTimer18 = createTimer(getMainForm())
freezeTimer18.Interval = 1000
freezeTimer18.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==18 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",3646)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",1)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",613)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",615)
--ProblyNotUsefullSinceNpcModel--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer18.destroy()
 end
 end
end
--FonctionForGnoll
if CCraceBar.position ==19 then
ourValue = nil
freezeTimer19 = createTimer(getMainForm())
freezeTimer19.Interval = 1000
freezeTimer19.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==19 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",23)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",24)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",25)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",26)
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer19.destroy()
 end
 end
end
--FonctionForOldMan
if CCraceBar.position ==20 then
ourValue = nil
freezeTimer20 = createTimer(getMainForm())
freezeTimer20.Interval = 1000
freezeTimer20.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==20 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",22)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",1)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",613)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",615)
--ProblyNotUsefullSinceNpcModel--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer20.destroy()
 end
 end
end
--FonctionForSnowGnobolt
if CCraceBar.position ==21 then
ourValue = nil
freezeTimer21 = createTimer(getMainForm())
freezeTimer21.Interval = 1000
freezeTimer21.onTimer = function(sender)
   if (not ourValue) then
      ourValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
   end
local currentValue = readSmallInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90')
 if CCraceBar.position ==21 and getProcessIDFromProcessName("cubeworld.exe") ~= nil then
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90",3252)
writeSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98",3254)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94",3253)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96",3251)
--ProblyNotUsefullSinceNpcModel--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+3B8",4)--ChestType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+3BC",1)--ChestSub
--writeBytes("[[[[[cubeworld.exe+00551A80]+8]+3C8]+8]+80]+458",0)--FeetType
--writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+45C",0)--FeetSub
   else -- everything is fine, and we should update ourValue to currentValue
      ourValue = currentValue
      freezeTimer21.destroy()
 end
    end
end
end



CCForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox4, 0)
   return caHide
end
function UDF1_CEToggleBox4Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox4) == 1) then
CCForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox4) == 0) then
CCForm.hide()
  end
end

--ModelForm
local modelForm = createForm(false)
modelForm.Caption='Model'
modelForm.Height = 500
modelForm.Width = 400
modelForm.Top = 380
modelForm.Left = 300
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(modelForm, [[ModelFormMain.png]])
PresetComboBox = createComboBox(modelForm)
PresetComboBox.Width = 100
PresetComboBox.top = 450
PresetComboBox.left = 150
PresetComboBoxitem = PresetComboBox.getItems
PresetComboBox.style = 'csDropDownList'
PresetComboBox.items.add("Preset: 1")
PresetComboBox.items.add("Preset: 2")
PresetComboBox.items.add("Preset: 3")
PresetComboBox.items.add("Preset: 4")
PresetComboBox.items.add("Preset: 5")
PresetComboBox.items.add("Preset: 6")
PresetComboBox.items.add("Preset: 7")
PresetComboBox.items.add("Preset: 8")
PresetComboBox.items.add("Preset: 9")
PresetComboBox.items.add("Preset: 10")
PresetComboBox.items.add("Preset: 11")
PresetComboBox.items.add("Preset: 12")
PresetComboBox.items.add("Preset: 13")
PresetComboBox.items.add("Preset: 14")
PresetComboBox.items.add("Preset: 15")
PresetComboBox.items.add("Preset: 16")
PresetComboBox.items.add("Preset: 17")
PresetComboBox.items.add("Preset: 18")
PresetComboBox.items.add("Preset: 19")
PresetComboBox.items.add("Preset: 20")
PresetSaveButton = createButton(modelForm)
PresetSaveButton.top = 452
PresetSaveButton.Caption = 'Save'
PresetSaveButton.Width = 30
PresetSaveButton.Height = 20
PresetSaveButton.left = 110
PresetSaveButton.OnClick = function (sender)
 if PresetComboBox.ItemIndex == 0 then
settings.Value['Mainedit'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 1 then
settings.Value['Mainedit-1'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-1'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-1'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-1'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-1'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-1'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-1'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-1'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-1'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-1'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-1'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-1'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-1'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-1'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-1'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-1'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-1'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-1'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-1'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-1'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-1'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-1'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-1'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-1'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-1'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-1'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-1'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-1'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-1'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-1'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-1'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-1'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-1'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-1'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-1'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-1'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-1'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-1'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-1'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-1'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-1'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-1'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-1'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-1'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 2 then
settings.Value['Mainedit-2'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-2'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-2'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-2'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-2'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-2'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-2'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-2'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-2'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-2'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-2'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-2'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-2'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-2'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-2'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-2'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-2'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-2'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-2'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-2'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-2'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-2'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-2'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-2'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-2'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-2'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-2'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-2'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-2'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-2'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-2'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-2'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-2'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-2'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-2'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-2'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-2'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-2'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-2'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-2'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-2'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-2'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-2'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-2'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 3 then
settings.Value['Mainedit-3'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-3'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-3'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-3'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-3'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-3'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-3'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-3'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-3'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-3'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-3'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-3'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-3'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-3'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-3'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-3'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-3'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-3'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-3'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-3'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-3'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-3'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-3'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-3'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-3'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-3'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-3'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-3'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-3'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-3'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-3'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-3'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-3'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-3'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-3'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-3'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-3'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-3'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-3'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-3'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-3'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-3'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-3'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-3'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 4 then
settings.Value['Mainedit-4'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-4'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-4'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-4'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-4'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-4'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-4'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-4'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-4'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-4'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-4'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-4'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-4'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-4'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-4'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-4'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-4'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-4'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-4'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-4'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-4'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-4'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-4'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-4'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-4'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-4'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-4'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-4'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-4'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-4'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-4'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-4'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-4'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-4'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-4'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-4'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-4'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-4'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-4'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-4'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-4'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-4'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-4'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-4'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 5 then
settings.Value['Mainedit-5'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-5'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-5'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-5'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-5'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-5'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-5'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-5'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-5'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-5'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-5'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-5'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-5'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-5'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-5'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-5'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-5'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-5'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-5'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-5'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-5'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-5'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-5'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-5'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-5'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-5'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-5'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-5'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-5'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-5'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-5'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-5'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-5'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-5'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-5'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-5'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-5'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-5'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-5'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-5'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-5'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-5'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-5'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-5'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 6 then
settings.Value['Mainedit-6'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-6'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-6'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-6'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-6'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-6'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-6'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-6'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-6'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-6'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-6'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-6'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-6'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-6'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-6'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-6'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-6'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-6'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-6'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-6'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-6'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-6'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-6'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-6'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-6'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-6'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-6'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-6'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-6'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-6'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-6'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-6'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-6'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-6'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-6'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-6'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-6'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-6'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-6'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-6'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-6'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-6'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-6'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-6'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 7 then
settings.Value['Mainedit-7'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-7'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-7'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-7'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-7'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-7'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-7'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-7'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-7'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-7'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-7'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-7'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-7'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-7'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-7'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-7'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-7'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-7'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-7'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-7'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-7'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-7'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-7'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-7'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-7'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-7'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-7'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-7'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-7'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-7'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-7'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-7'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-7'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-7'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-7'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-7'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-7'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-7'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-7'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-7'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-7'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-7'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-7'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-7'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 8 then
settings.Value['Mainedit-8'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-8'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-8'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-8'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-8'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-8'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-8'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-8'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-8'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-8'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-8'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-8'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-8'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-8'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-8'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-8'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-8'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-8'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-8'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-8'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-8'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-8'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-8'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-8'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-8'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-8'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-8'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-8'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-8'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-8'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-8'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-8'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-8'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-8'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-8'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-8'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-8'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-8'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-8'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-8'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-8'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-8'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-8'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-8'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 9 then
settings.Value['Mainedit-9'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-9'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-9'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-9'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-9'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-9'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-9'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-9'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-9'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-9'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-9'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-9'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-9'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-9'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-9'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-9'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-9'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-9'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-9'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-9'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-9'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-9'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-9'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-9'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-9'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-9'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-9'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-9'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-9'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-9'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-9'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-9'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-9'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-9'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-9'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-9'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-9'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-9'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-9'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-9'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-9'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-9'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-9'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-9'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 10 then
settings.Value['Mainedit-10'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-10'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-10'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-10'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-10'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-10'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-10'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-10'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-10'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-10'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-10'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-10'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-10'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-10'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-10'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-10'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-10'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-10'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-10'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-10'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-10'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-10'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-10'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-10'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-10'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-10'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-10'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-10'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-10'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-10'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-10'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-10'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-10'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-10'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-10'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-10'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-10'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-10'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-10'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-10'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-10'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-10'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-10'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-10'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 11 then
settings.Value['Mainedit-11'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-11'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-11'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-11'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-11'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-11'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-11'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-11'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-11'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-11'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-11'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-11'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-11'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-11'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-11'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-11'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-11'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-11'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-11'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-11'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-11'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-11'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-11'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-11'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-11'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-11'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-11'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-11'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-11'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-11'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-11'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-11'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-11'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-11'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-11'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-11'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-11'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-11'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-11'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-11'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-11'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-11'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-11'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-11'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 12 then
settings.Value['Mainedit-12'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-12'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-12'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-12'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-12'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-12'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-12'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-12'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-12'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-12'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-12'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-12'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-12'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-12'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-12'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-12'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-12'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-12'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-12'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-12'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-12'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-12'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-12'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-12'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-12'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-12'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-12'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-12'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-12'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-12'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-12'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-12'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-12'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-12'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-12'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-12'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-12'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-12'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-12'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-12'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-12'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-12'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-12'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-12'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 13 then
settings.Value['Mainedit-13'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-13'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-13'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-13'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-13'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-13'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-13'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-13'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-13'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-13'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-13'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-13'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-13'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-13'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-13'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-13'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-13'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-13'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-13'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-13'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-13'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-13'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-13'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-13'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-13'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-13'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-13'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-13'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-13'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-13'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-13'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-13'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-13'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-13'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-13'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-13'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-13'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-13'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-13'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-13'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-13'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-13'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-13'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-13'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 14 then
settings.Value['Mainedit-14'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-14'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-14'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-14'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-14'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-14'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-14'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-14'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-14'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-14'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-14'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-14'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-14'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-14'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-14'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-14'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-14'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-14'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-14'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-14'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-14'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-14'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-14'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-14'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-14'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-14'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-14'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-14'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-14'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-14'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-14'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-14'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-14'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-14'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-14'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-14'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-14'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-14'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-14'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-14'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-14'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-14'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-14'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-14'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 15 then
settings.Value['Mainedit-15'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-15'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-15'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-15'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-15'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-15'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-15'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-15'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-15'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-15'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-15'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-15'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-15'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-15'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-15'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-15'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-15'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-15'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-15'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-15'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-15'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-15'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-15'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-15'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-15'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-15'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-15'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-15'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-15'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-15'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-15'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-15'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-15'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-15'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-15'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-15'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-15'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-15'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-15'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-15'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-15'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-15'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-15'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-15'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 16 then
settings.Value['Mainedit-16'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-16'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-16'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-16'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-16'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-16'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-16'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-16'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-16'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-16'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-16'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-16'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-16'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-16'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-16'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-16'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-16'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-16'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-16'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-16'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-16'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-16'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-16'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-16'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-16'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-16'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-16'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-16'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-16'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-16'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-16'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-16'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-16'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-16'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-16'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-16'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-16'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-16'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-16'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-16'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-16'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-16'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-16'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-16'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 17 then
settings.Value['Mainedit-17'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-17'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-17'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-17'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-17'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-17'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-17'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-17'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-17'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-17'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-17'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-17'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-17'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-17'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-17'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-17'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-17'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-17'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-17'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-17'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-17'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-17'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-17'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-17'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-17'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-17'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-17'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-17'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-17'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-17'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-17'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-17'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-17'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-17'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-17'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-17'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-17'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-17'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-17'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-17'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-17'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-17'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-17'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-17'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 18 then
settings.Value['Mainedit-18'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-18'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-18'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-18'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-18'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-18'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-18'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-18'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-18'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-18'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-18'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-18'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-18'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-18'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-18'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-18'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-18'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-18'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-18'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-18'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-18'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-18'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-18'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-18'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-18'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-18'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-18'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-18'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-18'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-18'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-18'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-18'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-18'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-18'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-18'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-18'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-18'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-18'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-18'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-18'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-18'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-18'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-18'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-18'] = getProperty(sliderHB3, 'Position')
 elseif PresetComboBox.ItemIndex == 19 then
settings.Value['Mainedit-19'] = getProperty(Mainedit, 'text')
settings.Value['Mainedit2-19'] = getProperty(Mainedit2, 'text')
settings.Value['Mainedit3-19'] = getProperty(Mainedit3, 'text')
settings.Value['Mainedit4-19'] = getProperty(Mainedit4, 'text')
settings.Value['Mainedit5-19'] = getProperty(Mainedit5, 'text')
settings.Value['Mainedit6-19'] = getProperty(Mainedit6, 'text')
settings.Value['Mainedit7-19'] = getProperty(Mainedit7, 'text')
settings.Value['Mainedit8-19'] = getProperty(Mainedit8, 'text')
settings.Value['BSedit-19'] = getProperty(sliderBS, 'Position')
settings.Value['BSedit2-19'] = getProperty(sliderBS2, 'Position')
settings.Value['BSedit3-19'] = getProperty(sliderBS3, 'Position')
settings.Value['BSedit4-19'] = getProperty(sliderBS4, 'Position')
settings.Value['BSedit5-19'] = getProperty(sliderBS5, 'Position')
settings.Value['BSedit6-19'] = getProperty(sliderBS6, 'Position')
settings.Value['BSedit7-19'] = getProperty(sliderBS7, 'Position')
settings.Value['BSedit8-19'] = getProperty(sliderBS8, 'Position')
settings.Value['BRedit2-19'] = getProperty(BRedit2, 'text')
settings.Value['BRedit3-19'] = getProperty(BRedit3, 'text')
settings.Value['BRedit4-19'] = getProperty(BRedit4, 'text')
settings.Value['BRedit5-19'] = getProperty(BRedit5, 'text')
settings.Value['BRedit6-19'] = getProperty(BRedit6, 'text')
settings.Value['BRedit7-19'] = getProperty(BRedit7, 'text')
settings.Value['BRedit8-19'] = getProperty(BRedit8, 'text')
settings.Value['BPeditX2-19'] = getProperty(sliderBPX, 'Position')
settings.Value['BPeditX3-19'] = getProperty(sliderBPX2, 'Position')
settings.Value['BPeditX4-19'] = getProperty(sliderBPX3, 'Position')
settings.Value['BPeditX5-19'] = getProperty(sliderBPX4, 'Position')
settings.Value['BPeditX6-19'] = getProperty(sliderBPX5, 'Position')
settings.Value['BPeditX7-19'] = getProperty(sliderBPX6, 'Position')
settings.Value['BPeditY2-19'] = getProperty(sliderBPY, 'Position')
settings.Value['BPeditY3-19'] = getProperty(sliderBPY2, 'Position')
settings.Value['BPeditY4-19'] = getProperty(sliderBPY3, 'Position')
settings.Value['BPeditY5-19'] = getProperty(sliderBPY4, 'Position')
settings.Value['BPeditY6-19'] = getProperty(sliderBPY5, 'Position')
settings.Value['BPeditY7-19'] = getProperty(sliderBPY6, 'Position')
settings.Value['BPeditZ2-19'] = getProperty(sliderBPZ, 'Position')
settings.Value['BPeditZ3-19'] = getProperty(sliderBPZ2, 'Position')
settings.Value['BPeditZ4-19'] = getProperty(sliderBPZ3, 'Position')
settings.Value['BPeditZ5-19'] = getProperty(sliderBPZ4, 'Position')
settings.Value['BPeditZ6-19'] = getProperty(sliderBPZ5, 'Position')
settings.Value['BPeditZ7-19'] = getProperty(sliderBPZ6, 'Position')
settings.Value['HBedit-19'] = getProperty(sliderHB, 'Position')
settings.Value['HBedit2-19'] = getProperty(sliderHB2, 'Position')
settings.Value['HBedit3-19'] = getProperty(sliderHB3, 'Position')
 end
end
PresetLoadButton = createButton(modelForm)
PresetLoadButton.top = 452
PresetLoadButton.Caption = 'Load'
PresetLoadButton.Width = 30
PresetLoadButton.Height = 20
PresetLoadButton.left = 260
PresetLoadButton.OnClick = function (sender)
 if PresetComboBox.ItemIndex == 0 then
 setProperty(slider, 'Position', settings.Value['Mainedit'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8'])
 setProperty(BSedit, 'Position', settings.Value['BSedit'])
 setProperty(BSedit2, 'Position', settings.Value['BSedit2'])
 setProperty(BSedit3, 'Position', settings.Value['BSedit3'])
 setProperty(BSedit4, 'Position', settings.Value['BSedit4'])
 setProperty(BSedit5, 'Position', settings.Value['BSedit5'])
 setProperty(BSedit6, 'Position', settings.Value['BSedit6'])
 setProperty(BSedit7, 'Position', settings.Value['BSedit7'])
 setProperty(BSedit8, 'Position', settings.Value['BSedit8'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3'])
 elseif PresetComboBox.ItemIndex == 1 then
 setProperty(slider, 'Position', settings.Value['Mainedit-1'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-1'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-1'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-1'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-1'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-1'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-1'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-1'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-1'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-1'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-1'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-1'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-1'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-1'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-1'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-1'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-1'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-1'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-1'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-1'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-1'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-1'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-1'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-1'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-1'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-1'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-1'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-1'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-1'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-1'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-1'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-1'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-1'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-1'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-1'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-1'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-1'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-1'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-1'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-1'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-1'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-1'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-1'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-1'])
 elseif PresetComboBox.ItemIndex == 2 then
 setProperty(slider, 'Position', settings.Value['Mainedit-2'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-2'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-2'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-2'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-2'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-2'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-2'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-2'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-2'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-2'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-2'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-2'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-2'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-2'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-2'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-2'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-2'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-2'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-2'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-2'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-2'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-2'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-2'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-2'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-2'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-2'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-2'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-2'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-2'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-2'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-2'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-2'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-2'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-2'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-2'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-2'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-2'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-2'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-2'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-2'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-2'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-2'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-2'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-2'])
  elseif PresetComboBox.ItemIndex == 3 then
 setProperty(slider, 'Position', settings.Value['Mainedit-3'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-3'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-3'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-3'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-3'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-3'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-3'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-3'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-3'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-3'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-3'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-3'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-3'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-3'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-3'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-3'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-3'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-3'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-3'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-3'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-3'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-3'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-3'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-3'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-3'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-3'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-3'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-3'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-3'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-3'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-3'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-3'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-3'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-3'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-3'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-3'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-3'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-3'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-3'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-3'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-3'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-3'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-3'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-3'])
 elseif PresetComboBox.ItemIndex == 4 then
 setProperty(slider, 'Position', settings.Value['Mainedit-4'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-4'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-4'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-4'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-4'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-4'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-4'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-4'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-4'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-4'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-4'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-4'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-4'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-4'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-4'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-4'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-4'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-4'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-4'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-4'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-4'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-4'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-4'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-4'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-4'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-4'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-4'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-4'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-4'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-4'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-4'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-4'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-4'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-4'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-4'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-4'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-4'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-4'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-4'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-4'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-4'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-4'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-4'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-4'])
elseif PresetComboBox.ItemIndex == 5 then
 setProperty(slider, 'Position', settings.Value['Mainedit-5'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-5'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-5'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-5'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-5'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-5'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-5'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-5'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-5'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-5'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-5'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-5'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-5'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-5'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-5'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-5'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-5'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-5'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-5'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-5'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-5'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-5'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-5'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-5'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-5'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-5'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-5'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-5'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-5'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-5'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-5'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-5'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-5'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-5'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-5'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-5'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-5'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-5'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-5'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-5'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-5'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-5'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-5'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-5'])
elseif PresetComboBox.ItemIndex == 6 then
 setProperty(slider, 'Position', settings.Value['Mainedit-6'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-6'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-6'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-6'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-6'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-6'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-6'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-6'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-6'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-6'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-6'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-6'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-6'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-6'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-6'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-6'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-6'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-6'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-6'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-6'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-6'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-6'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-6'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-6'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-6'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-6'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-6'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-6'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-6'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-6'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-6'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-6'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-6'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-6'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-6'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-6'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-6'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-6'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-6'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-6'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-6'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-6'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-6'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-6'])
elseif PresetComboBox.ItemIndex == 7 then
 setProperty(slider, 'Position', settings.Value['Mainedit-7'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-7'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-7'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-7'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-7'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-7'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-7'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-7'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-7'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-7'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-7'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-7'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-7'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-7'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-7'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-7'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-7'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-7'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-7'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-7'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-7'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-7'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-7'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-7'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-7'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-7'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-7'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-7'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-7'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-7'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-7'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-7'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-7'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-7'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-7'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-7'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-7'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-7'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-7'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-7'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-7'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-7'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-7'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-7'])
elseif PresetComboBox.ItemIndex == 8 then
 setProperty(slider, 'Position', settings.Value['Mainedit-8'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-8'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-8'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-8'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-8'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-8'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-8'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-8'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-8'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-8'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-8'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-8'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-8'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-8'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-8'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-8'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-8'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-8'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-8'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-8'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-8'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-8'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-8'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-8'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-8'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-8'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-8'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-8'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-8'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-8'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-8'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-8'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-8'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-8'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-8'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-8'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-8'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-8'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-8'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-8'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-8'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-8'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-8'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-8'])
 elseif PresetComboBox.ItemIndex == 9 then
 setProperty(slider, 'Position', settings.Value['Mainedit-9'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-9'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-9'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-9'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-9'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-9'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-9'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-9'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-9'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-9'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-9'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-9'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-9'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-9'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-9'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-9'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-9'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-9'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-9'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-9'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-9'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-9'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-9'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-9'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-9'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-9'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-9'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-9'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-9'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-9'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-9'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-9'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-9'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-9'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-9'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-9'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-9'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-9'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-9'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-9'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-9'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-9'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-9'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-9'])
 elseif PresetComboBox.ItemIndex == 10 then
 setProperty(slider, 'Position', settings.Value['Mainedit-10'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-10'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-10'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-10'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-10'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-10'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-10'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-10'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-10'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-10'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-10'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-10'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-10'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-10'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-10'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-10'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-10'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-10'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-10'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-10'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-10'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-10'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-10'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-10'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-10'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-10'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-10'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-10'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-10'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-10'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-10'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-10'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-10'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-10'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-10'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-10'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-10'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-10'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-10'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-10'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-10'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-10'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-10'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-10'])
 elseif PresetComboBox.ItemIndex == 11 then
 setProperty(slider, 'Position', settings.Value['Mainedit-11'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-11'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-11'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-11'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-11'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-11'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-11'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-11'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-11'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-11'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-11'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-11'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-11'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-11'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-11'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-11'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-11'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-11'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-11'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-11'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-11'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-11'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-11'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-11'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-11'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-11'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-11'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-11'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-11'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-11'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-11'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-11'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-11'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-11'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-11'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-11'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-11'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-11'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-11'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-11'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-11'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-11'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-11'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-11'])
 elseif PresetComboBox.ItemIndex == 12 then
 setProperty(slider, 'Position', settings.Value['Mainedit-12'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-12'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-12'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-12'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-12'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-12'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-12'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-12'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-12'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-12'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-12'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-12'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-12'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-12'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-12'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-12'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-12'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-12'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-12'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-12'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-12'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-12'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-12'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-12'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-12'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-12'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-12'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-12'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-12'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-12'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-12'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-12'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-12'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-12'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-12'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-12'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-12'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-12'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-12'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-12'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-12'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-12'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-12'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-12'])
 elseif PresetComboBox.ItemIndex == 13 then
 setProperty(slider, 'Position', settings.Value['Mainedit-13'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-13'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-13'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-13'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-13'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-13'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-13'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-13'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-13'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-13'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-13'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-13'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-13'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-13'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-13'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-13'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-13'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-13'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-13'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-13'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-13'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-13'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-13'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-13'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-13'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-13'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-13'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-13'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-13'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-13'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-13'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-13'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-13'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-13'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-13'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-13'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-13'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-13'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-13'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-13'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-13'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-13'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-13'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-13'])
 elseif PresetComboBox.ItemIndex == 14 then
 setProperty(slider, 'Position', settings.Value['Mainedit-14'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-14'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-14'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-14'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-14'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-14'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-14'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-14'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-14'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-14'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-14'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-14'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-14'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-14'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-14'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-14'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-14'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-14'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-14'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-14'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-14'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-14'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-14'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-14'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-14'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-14'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-14'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-14'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-14'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-14'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-14'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-14'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-14'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-14'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-14'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-14'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-14'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-14'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-14'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-14'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-14'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-14'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-14'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-14'])
 elseif PresetComboBox.ItemIndex == 15 then
 setProperty(slider, 'Position', settings.Value['Mainedit-15'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-15'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-15'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-15'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-15'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-15'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-15'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-15'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-15'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-15'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-15'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-15'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-15'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-15'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-15'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-15'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-15'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-15'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-15'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-15'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-15'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-15'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-15'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-15'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-15'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-15'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-15'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-15'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-15'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-15'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-15'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-15'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-15'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-15'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-15'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-15'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-15'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-15'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-15'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-15'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-15'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-15'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-15'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-15'])
 elseif PresetComboBox.ItemIndex == 16 then
 setProperty(slider, 'Position', settings.Value['Mainedit-16'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-16'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-16'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-16'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-16'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-16'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-16'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-16'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-16'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-16'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-16'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-16'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-16'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-16'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-16'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-16'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-16'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-16'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-16'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-16'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-16'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-16'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-16'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-16'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-16'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-16'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-16'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-16'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-16'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-16'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-16'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-16'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-16'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-16'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-16'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-16'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-16'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-16'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-16'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-16'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-16'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-16'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-16'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-16'])
 elseif PresetComboBox.ItemIndex == 17 then
 setProperty(slider, 'Position', settings.Value['Mainedit-17'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-17'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-17'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-17'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-17'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-17'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-17'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-17'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-17'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-17'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-17'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-17'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-17'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-17'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-17'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-17'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-17'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-17'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-17'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-17'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-17'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-17'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-17'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-17'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-17'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-17'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-17'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-17'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-17'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-17'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-17'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-17'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-17'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-17'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-17'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-17'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-17'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-17'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-17'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-17'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-17'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-17'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-17'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-17'])
 elseif PresetComboBox.ItemIndex == 18 then
 setProperty(slider, 'Position', settings.Value['Mainedit-18'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-18'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-18'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-18'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-18'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-18'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-18'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-18'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-18'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-18'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-18'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-18'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-18'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-18'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-18'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-18'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-18'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-18'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-18'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-18'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-18'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-18'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-18'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-18'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-18'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-18'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-18'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-18'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-18'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-18'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-18'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-18'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-18'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-18'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-18'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-18'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-18'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-18'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-18'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-18'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-18'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-18'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-18'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-18'])
 elseif PresetComboBox.ItemIndex == 19 then
 setProperty(slider, 'Position', settings.Value['Mainedit-19'])
 setProperty(slider2, 'Position', settings.Value['Mainedit2-19'])
 setProperty(slider3, 'Position', settings.Value['Mainedit3-19'])
 setProperty(slider4, 'Position', settings.Value['Mainedit4-19'])
 setProperty(slider5, 'Position', settings.Value['Mainedit5-19'])
 setProperty(slider6, 'Position', settings.Value['Mainedit6-19'])
 setProperty(slider7, 'Position', settings.Value['Mainedit7-19'])
 setProperty(slider8, 'Position', settings.Value['Mainedit8-19'])
 setProperty(sliderBS, 'Position', settings.Value['BSedit-19'])
 setProperty(sliderBS2, 'Position', settings.Value['BSedit2-19'])
 setProperty(sliderBS3, 'Position', settings.Value['BSedit3-19'])
 setProperty(sliderBS4, 'Position', settings.Value['BSedit4-19'])
 setProperty(sliderBS5, 'Position', settings.Value['BSedit5-19'])
 setProperty(sliderBS6, 'Position', settings.Value['BSedit6-19'])
 setProperty(sliderBS7, 'Position', settings.Value['BSedit7-19'])
 setProperty(sliderBS8, 'Position', settings.Value['BSedit8-19'])
 setProperty(sliderBR2, 'Position', settings.Value['BRedit2-19'])
 setProperty(sliderBR3, 'Position', settings.Value['BRedit3-19'])
 setProperty(sliderBR4, 'Position', settings.Value['BRedit4-19'])
 setProperty(sliderBR5, 'Position', settings.Value['BRedit5-19'])
 setProperty(sliderBR6, 'Position', settings.Value['BRedit6-19'])
 setProperty(sliderBR7, 'Position', settings.Value['BRedit7-19'])
 setProperty(sliderBR8, 'Position', settings.Value['BRedit8-19'])
 setProperty(sliderBPX, 'Position', settings.Value['BPeditX2-19'])
 setProperty(sliderBPX2, 'Position', settings.Value['BPeditX3-19'])
 setProperty(sliderBPX3, 'Position', settings.Value['BPeditX4-19'])
 setProperty(sliderBPX4, 'Position', settings.Value['BPeditX5-19'])
 setProperty(sliderBPX5, 'Position', settings.Value['BPeditX6-19'])
 setProperty(sliderBPX6, 'Position', settings.Value['BPeditX7-19'])
 setProperty(sliderBPY, 'Position', settings.Value['BPeditY2-19'])
 setProperty(sliderBPY2, 'Position', settings.Value['BPeditY3-19'])
 setProperty(sliderBPY3, 'Position', settings.Value['BPeditY4-19'])
 setProperty(sliderBPY4, 'Position', settings.Value['BPeditY5-19'])
 setProperty(sliderBPY5, 'Position', settings.Value['BPeditY6-19'])
 setProperty(sliderBPY6, 'Position', settings.Value['BPeditY7-19'])
 setProperty(sliderBPZ, 'Position', settings.Value['BPeditZ2-19'])
 setProperty(sliderBPZ2, 'Position', settings.Value['BPeditZ3-19'])
 setProperty(sliderBPZ3, 'Position', settings.Value['BPeditZ4-19'])
 setProperty(sliderBPZ4, 'Position', settings.Value['BPeditZ5-19'])
 setProperty(sliderBPZ5, 'Position', settings.Value['BPeditZ6-19'])
 setProperty(sliderBPZ6, 'Position', settings.Value['BPeditZ7-19'])
 setProperty(sliderHB, 'Position', settings.Value['HBedit-19'])
 setProperty(sliderHB2, 'Position', settings.Value['HBedit2-19'])
 setProperty(sliderHB3, 'Position', settings.Value['HBedit3-19'])
 end
end
toggle=createToggleBox(modelForm)
checkbox_setState(toggle, 1)
toggle.Caption='Main'
toggle.Left = 10
toggle.OnChange = function (sender)
  if (checkbox_getState(toggle) == 1) then
   checkbox_setState(toggleBS, 0)
   checkbox_setState(toggleBR, 0)
   checkbox_setState(toggleBP, 0)
   checkbox_setState(toggleHB, 0)
   slider.Visible = true
   slider2.Visible = true
   slider3.Visible = true
   slider4.Visible = true
   slider5.Visible = true
   slider6.Visible = true
   slider7.Visible = true
   slider8.Visible = true
   MainHair.Visible = true
   MainFace.Visible = true
   MainHands.Visible = true
   MainFeet.Visible = true
   MainChest.Visible = true
   MainShoul.Visible = true
   MainBack.Visible = true
   MainWings.Visible = true
   Mainedit.Visible = true
   Mainedit2.Visible = true
   Mainedit3.Visible = true
   Mainedit4.Visible = true
   Mainedit5.Visible = true
   Mainedit6.Visible = true
   Mainedit7.Visible = true
   Mainedit8.Visible = true
  elseif (checkbox_getState(toggle) == 0) then
   slider.Visible = false
   slider2.Visible = false
   slider3.Visible = false
   slider4.Visible = false
   slider5.Visible = false
   slider6.Visible = false
   slider7.Visible = false
   slider8.Visible = false
   MainHair.Visible = false
   MainFace.Visible = false
   MainHands.Visible = false
   MainFeet.Visible = false
   MainChest.Visible = false
   MainShoul.Visible = false
   MainBack.Visible = false
   MainWings.Visible = false
   Mainedit.Visible = false
   Mainedit2.Visible = false
   Mainedit3.Visible = false
   Mainedit4.Visible = false
   Mainedit5.Visible = false
   Mainedit6.Visible = false
   Mainedit7.Visible = false
   Mainedit8.Visible = false
  end
end
toggleBS=createToggleBox(modelForm)
toggleBS.Caption='BodySizes'
toggleBS.Left = 85
toggleBS.OnClick = function (sender)
  if(checkbox_getState(toggleBS) == 1) then
   checkbox_setState(toggle, 0)
   checkbox_setState(toggleBR, 0)
   checkbox_setState(toggleBP, 0)
   checkbox_setState(toggleHB, 0)
   sliderBS.Visible = true
   sliderBS2.Visible = true
   sliderBS3.Visible = true
   sliderBS4.Visible = true
   sliderBS5.Visible = true
   sliderBS6.Visible = true
   sliderBS7.Visible = true
   sliderBS8.Visible = true
   SizeHead.Visible = true
   SizeChest.Visible = true
   SizeHands.Visible = true
   SizeFeet.Visible = true
   SizeShoul.Visible = true
   SizeBack.Visible = true
   SizeWings.Visible = true
   SizeWeap.Visible = true
   BSedit.Visible = true
   BSedit2.Visible = true
   BSedit3.Visible = true
   BSedit4.Visible = true
   BSedit5.Visible = true
   BSedit6.Visible = true
   BSedit7.Visible = true
   BSedit8.Visible = true
  elseif (checkbox_getState(toggleBS) == 0) then
   sliderBS.Visible = false
   sliderBS2.Visible = false
   sliderBS3.Visible = false
   sliderBS4.Visible = false
   sliderBS5.Visible = false
   sliderBS6.Visible = false
   sliderBS7.Visible = false
   sliderBS8.Visible = false
   SizeHead.Visible = false
   SizeChest.Visible = false
   SizeHands.Visible = false
   SizeFeet.Visible = false
   SizeShoul.Visible = false
   SizeBack.Visible = false
   SizeWings.Visible = false
   SizeWeap.Visible = false
   BSedit.Visible = false
   BSedit2.Visible = false
   BSedit3.Visible = false
   BSedit4.Visible = false
   BSedit5.Visible = false
   BSedit6.Visible = false
   BSedit7.Visible = false
   BSedit8.Visible = false
  end
end
toggleBR=createToggleBox(modelForm)
toggleBR.Caption='Rotations'
toggleBR.Left = 160
toggleBR.OnClick = function (sender)
  if(checkbox_getState(toggleBR) == 1) then
   checkbox_setState(toggle, 0)
   checkbox_setState(toggleBS, 0)
   checkbox_setState(toggleBP, 0)
   checkbox_setState(toggleHB, 0)
   sliderBR2.Visible = true
   sliderBR3.Visible = true
   sliderBR4.Visible = true
   sliderBR5.Visible = true
   sliderBR6.Visible = true
   sliderBR7.Visible = true
   sliderBR8.Visible = true
   RotationChestZY.Visible = true
   RotationHandsZY.Visible = true
   RotationHandsXY.Visible = true
   RotationHandsZX.Visible = true
   RotationFeetZY.Visible = true
   RotationWingsZY.Visible = true
   RotationBackZY.Visible = true
   BRedit2.Visible = true
   BRedit3.Visible = true
   BRedit4.Visible = true
   BRedit5.Visible = true
   BRedit6.Visible = true
   BRedit7.Visible = true
   BRedit8.Visible = true
  elseif (checkbox_getState(toggleBR) == 0) then
   sliderBR2.Visible = false
   sliderBR3.Visible = false
   sliderBR4.Visible = false
   sliderBR5.Visible = false
   sliderBR6.Visible = false
   sliderBR7.Visible = false
   sliderBR8.Visible = false
   RotationChestZY.Visible = false
   RotationHandsZY.Visible = false
   RotationHandsXY.Visible = false
   RotationHandsZX.Visible = false
   RotationFeetZY.Visible = false
   RotationWingsZY.Visible = false
   RotationBackZY.Visible = false
   BRedit2.Visible = false
   BRedit3.Visible = false
   BRedit4.Visible = false
   BRedit5.Visible = false
   BRedit6.Visible = false
   BRedit7.Visible = false
   BRedit8.Visible = false
  end
end
toggleBP=createToggleBox(modelForm)
toggleBP.Caption='Positions'
toggleBP.Left = 235
toggleBP.OnClick = function (sender)
  if(checkbox_getState(toggleBP) == 1) then
   checkbox_setState(toggle, 0)
   checkbox_setState(toggleBS, 0)
   checkbox_setState(toggleBR, 0)
   checkbox_setState(toggleHB, 0)
   sliderBPX.Visible = true
   sliderBPX2.Visible = true
   sliderBPX3.Visible = true
   sliderBPX4.Visible = true
   sliderBPX5.Visible = true
   sliderBPX6.Visible = true
   sliderBPY1.Visible = true
   sliderBPY2.Visible = true
   sliderBPY3.Visible = true
   sliderBPY4.Visible = true
   sliderBPY5.Visible = true
   sliderBPY6.Visible = true
   sliderBPZ1.Visible = true
   sliderBPZ2.Visible = true
   sliderBPZ3.Visible = true
   sliderBPZ4.Visible = true
   sliderBPZ5.Visible = true
   sliderBPZ6.Visible = true
   PositionCentralBody.Visible = true
   PositionHead.Visible = true
   PositionHands.Visible = true
   PositionFeet.Visible = true
   PositionWings.Visible = true
   PositionBack.Visible = true
   PositionCentralBodyx.Visible = true
   PositionHeadx.Visible = true
   PositionHandsx.Visible = true
   PositionFeetx.Visible = true
   PositionWingsx.Visible = true
   PositionBackx.Visible = true
   PositionCentralBodyy.Visible = true
   PositionHeady.Visible = true
   PositionHandsy.Visible = true
   PositionFeety.Visible = true
   PositionWingsy.Visible = true
   PositionBacky.Visible = true
   PositionCentralBodyz.Visible = true
   PositionHeadz.Visible = true
   PositionHandsz.Visible = true
   PositionFeetz.Visible = true
   PositionWingsz.Visible = true
   PositionBackz.Visible = true
   BPeditX2.Visible = true
   BPeditX3.Visible = true
   BPeditX4.Visible = true
   BPeditX5.Visible = true
   BPeditX6.Visible = true
   BPeditX7.Visible = true
   BPeditY2.Visible = true
   BPeditY3.Visible = true
   BPeditY4.Visible = true
   BPeditY5.Visible = true
   BPeditY6.Visible = true
   BPeditY7.Visible = true
   BPeditZ2.Visible = true
   BPeditZ3.Visible = true
   BPeditZ4.Visible = true
   BPeditZ5.Visible = true
   BPeditZ6.Visible = true
   BPeditZ7.Visible = true
  elseif (checkbox_getState(toggleBP) == 0) then
  sliderBPX.Visible = false
  sliderBPX2.Visible = false
  sliderBPX3.Visible = false
  sliderBPX4.Visible = false
  sliderBPX5.Visible = false
  sliderBPX6.Visible = false
  sliderBPY1.Visible = false
  sliderBPY2.Visible = false
  sliderBPY3.Visible = false
  sliderBPY4.Visible = false
  sliderBPY5.Visible = false
  sliderBPY6.Visible = false
  sliderBPZ1.Visible = false
  sliderBPZ2.Visible = false
  sliderBPZ3.Visible = false
  sliderBPZ4.Visible = false
  sliderBPZ5.Visible = false
  sliderBPZ6.Visible = false
  PositionCentralBody.Visible = false
  PositionHead.Visible = false
  PositionHands.Visible = false
  PositionFeet.Visible = false
  PositionWings.Visible = false
  PositionBack.Visible = false
  PositionCentralBodyx.Visible = false
  PositionHeadx.Visible = false
  PositionHandsx.Visible = false
  PositionFeetx.Visible = false
  PositionWingsx.Visible = false
  PositionBackx.Visible = false
  PositionCentralBodyy.Visible = false
  PositionHeady.Visible = false
  PositionHandsy.Visible = false
  PositionFeety.Visible = false
  PositionWingsy.Visible = false
  PositionBacky.Visible = false
  PositionCentralBodyz.Visible = false
  PositionHeadz.Visible = false
  PositionHandsz.Visible = false
  PositionFeetz.Visible = false
  PositionWingsz.Visible = false
  PositionBackz.Visible = false
  BPeditX2.Visible = false
  BPeditX3.Visible = false
  BPeditX4.Visible = false
  BPeditX5.Visible = false
  BPeditX6.Visible = false
  BPeditX7.Visible = false
  BPeditY2.Visible = false
  BPeditY3.Visible = false
  BPeditY4.Visible = false
  BPeditY5.Visible = false
  BPeditY6.Visible = false
  BPeditY7.Visible = false
  BPeditZ2.Visible = false
  BPeditZ3.Visible = false
  BPeditZ4.Visible = false
  BPeditZ5.Visible = false
  BPeditZ6.Visible = false
  BPeditZ7.Visible = false
  end
end
toggleHB=createToggleBox(modelForm)
toggleHB.Caption='Hitbox'
toggleHB.Left = 310
toggleHB.OnClick = function (sender)
  if(checkbox_getState(toggleHB) == 1) then
   checkbox_setState(toggle, 0)
   checkbox_setState(toggleBS, 0)
   checkbox_setState(toggleBP, 0)
   checkbox_setState(toggleBR, 0)
   sliderHB.Visible = true
   sliderHB2.Visible = true
   sliderHB3.Visible = true
   HBHeight.Visible = true
   HBScaleHeight.Visible = true
   HBScaleWidth.Visible = true
   HBedit.Visible = true
   HBedit2.Visible = true
   HBedit3.Visible = true
  elseif (checkbox_getState(toggleHB) == 0) then
   sliderHB.Visible = false
   sliderHB2.Visible = false
   sliderHB3.Visible = false
   HBHeight.Visible = false
   HBScaleHeight.Visible = false
   HBScaleWidth.Visible = false
   HBedit.Visible = false
   HBedit2.Visible = false
   HBedit3.Visible = false
  end
end
slider=createTrackBar(modelForm)
slider.Width = 300
slider.Height = 25
slider.Left = 50
slider.Top = 50
slider.Max = 3652
slider.Min = 0
slider2=createTrackBar(modelForm)
slider2.Width = 300
slider2.Height = 25
slider2.Left = 50
slider2.Top = 100
slider2.Max = 3652
slider2.Min = 0
slider3=createTrackBar(modelForm)
slider3.Width = 300
slider3.Height = 25
slider3.Left = 50
slider3.Top = 150
slider3.Max = 3652
slider3.Min = 0
slider4=createTrackBar(modelForm)
slider4.Width = 300
slider4.Height = 25
slider4.Left = 50
slider4.Top = 200
slider4.Max = 3652
slider4.Min = 0
slider5=createTrackBar(modelForm)
slider5.Width = 300
slider5.Height = 25
slider5.Left = 50
slider5.Top = 250
slider5.Max = 3652
slider5.Min = 0
slider6=createTrackBar(modelForm)
slider6.Width = 300
slider6.Height = 25
slider6.Left = 50
slider6.Top = 300
slider6.Max = 3652
slider6.Min = 0
slider7=createTrackBar(modelForm)
slider7.Width = 300
slider7.Height = 25
slider7.Left = 50
slider7.Top = 350
slider7.Max = 3652
slider7.Min = 0
slider8=createTrackBar(modelForm)
slider8.Width = 300
slider8.Height = 25
slider8.Left = 50
slider8.Top = 400
slider8.Max = 3652
slider8.Min = 0
sliderBR2=createTrackBar(modelForm)
sliderBR2.Width = 300
sliderBR2.Height = 25
sliderBR2.Left = 50
sliderBR2.Top = 100
sliderBR2.Max = 180
sliderBR2.Min = -180
sliderBR3=createTrackBar(modelForm)
sliderBR3.Width = 300
sliderBR3.Height = 25
sliderBR3.Left = 50
sliderBR3.Top = 150
sliderBR3.Max = 180
sliderBR3.Min = -180
sliderBR4=createTrackBar(modelForm)
sliderBR4.Width = 300
sliderBR4.Height = 25
sliderBR4.Left = 50
sliderBR4.Top = 200
sliderBR4.Max = 180
sliderBR4.Min = -180
sliderBR5=createTrackBar(modelForm)
sliderBR5.Width = 300
sliderBR5.Height = 25
sliderBR5.Left = 50
sliderBR5.Top = 250
sliderBR5.Max = 180
sliderBR5.Min = -180
sliderBR6=createTrackBar(modelForm)
sliderBR6.Width = 300
sliderBR6.Height = 25
sliderBR6.Left = 50
sliderBR6.Top = 300
sliderBR6.Max = 180
sliderBR6.Min = -180
sliderBR7=createTrackBar(modelForm)
sliderBR7.Width = 300
sliderBR7.Height = 25
sliderBR7.Left = 50
sliderBR7.Top = 350
sliderBR7.Max = 180
sliderBR7.Min = -180
sliderBR8=createTrackBar(modelForm)
sliderBR8.Width = 300
sliderBR8.Height = 25
sliderBR8.Left = 50
sliderBR8.Top = 400
sliderBR8.Max = 180
sliderBR8.Min = -180
sliderBR2.Visible = false
sliderBR3.Visible = false
sliderBR4.Visible = false
sliderBR5.Visible = false
sliderBR6.Visible = false
sliderBR7.Visible = false
sliderBR8.Visible = false
sliderBS=createTrackBar(modelForm)
sliderBS.Width = 300
sliderBS.Height = 25
sliderBS.Left = 50
sliderBS.Top = 50
sliderBS.Max = 250
sliderBS.Min = 0
sliderBS2=createTrackBar(modelForm)
sliderBS2.Width = 300
sliderBS2.Height = 25
sliderBS2.Left = 50
sliderBS2.Top = 100
sliderBS2.Max = 250
sliderBS2.Min = 0
sliderBS3=createTrackBar(modelForm)
sliderBS3.Width = 300
sliderBS3.Height = 25
sliderBS3.Left = 50
sliderBS3.Top = 150
sliderBS3.Max = 250
sliderBS3.Min = 0
sliderBS4=createTrackBar(modelForm)
sliderBS4.Width = 300
sliderBS4.Height = 25
sliderBS4.Left = 50
sliderBS4.Top = 200
sliderBS4.Max = 250
sliderBS4.Min = 0
sliderBS5=createTrackBar(modelForm)
sliderBS5.Width = 300
sliderBS5.Height = 25
sliderBS5.Left = 50
sliderBS5.Top = 250
sliderBS5.Max = 250
sliderBS5.Min = 0
sliderBS6=createTrackBar(modelForm)
sliderBS6.Width = 300
sliderBS6.Height = 25
sliderBS6.Left = 50
sliderBS6.Top = 300
sliderBS6.Max = 250
sliderBS6.Min = 0
sliderBS7=createTrackBar(modelForm)
sliderBS7.Width = 300
sliderBS7.Height = 25
sliderBS7.Left = 50
sliderBS7.Top = 350
sliderBS7.Max = 250
sliderBS7.Min = 0
sliderBS8=createTrackBar(modelForm)
sliderBS8.Width = 300
sliderBS8.Height = 25
sliderBS8.Left = 50
sliderBS8.Top = 400
sliderBS8.Max = 250
sliderBS8.Min = 0
sliderBS.Visible = false
sliderBS2.Visible = false
sliderBS3.Visible = false
sliderBS4.Visible = false
sliderBS5.Visible = false
sliderBS6.Visible = false
sliderBS7.Visible = false
sliderBS8.Visible = false
sliderBPX=createTrackBar(modelForm)
sliderBPX.Width = 125
sliderBPX.Height = 25
sliderBPX.Left = 10
sliderBPX.Top = 70
sliderBPX.Max = 100
sliderBPX.Min = -100
sliderBPX2=createTrackBar(modelForm)
sliderBPX2.Width = 125
sliderBPX2.Height = 25
sliderBPX2.Left = 10
sliderBPX2.Top = 140
sliderBPX2.Max = 100
sliderBPX2.Min = -100
sliderBPX3=createTrackBar(modelForm)
sliderBPX3.Width = 125
sliderBPX3.Height = 25
sliderBPX3.Left = 10
sliderBPX3.Top = 210
sliderBPX3.Max = 100
sliderBPX3.Min = -100
sliderBPX4=createTrackBar(modelForm)
sliderBPX4.Width = 125
sliderBPX4.Height = 25
sliderBPX4.Left = 10
sliderBPX4.Top = 280
sliderBPX4.Max = 100
sliderBPX4.Min = -100
sliderBPX5=createTrackBar(modelForm)
sliderBPX5.Width = 125
sliderBPX5.Height = 25
sliderBPX5.Left = 10
sliderBPX5.Top = 350
sliderBPX5.Max = 100
sliderBPX5.Min = -100
sliderBPX6=createTrackBar(modelForm)
sliderBPX6.Width = 125
sliderBPX6.Height = 25
sliderBPX6.Left = 10
sliderBPX6.Top = 420
sliderBPX6.Max = 100
sliderBPX6.Min = -100
sliderBPY1=createTrackBar(modelForm)
sliderBPY1.Width = 125
sliderBPY1.Height = 25
sliderBPY1.Left = 140
sliderBPY1.Top = 70
sliderBPY1.Max = 100
sliderBPY1.Min = -100
sliderBPY2=createTrackBar(modelForm)
sliderBPY2.Width = 125
sliderBPY2.Height = 25
sliderBPY2.Left = 140
sliderBPY2.Top = 140
sliderBPY2.Max = 100
sliderBPY2.Min = -100
sliderBPY3=createTrackBar(modelForm)
sliderBPY3.Width = 125
sliderBPY3.Height = 25
sliderBPY3.Left = 140
sliderBPY3.Top = 210
sliderBPY3.Max = 100
sliderBPY3.Min = -100
sliderBPY4=createTrackBar(modelForm)
sliderBPY4.Width = 125
sliderBPY4.Height = 25
sliderBPY4.Left = 140
sliderBPY4.Top = 280
sliderBPY4.Max = 100
sliderBPY4.Min = -100
sliderBPY5=createTrackBar(modelForm)
sliderBPY5.Width = 125
sliderBPY5.Height = 25
sliderBPY5.Left = 140
sliderBPY5.Top = 350
sliderBPY5.Max = 100
sliderBPY5.Min = -100
sliderBPY6=createTrackBar(modelForm)
sliderBPY6.Width = 125
sliderBPY6.Height = 25
sliderBPY6.Left = 140
sliderBPY6.Top = 420
sliderBPY6.Max = 100
sliderBPY6.Min = -100
sliderBPZ1=createTrackBar(modelForm)
sliderBPZ1.Width = 125
sliderBPZ1.Height = 25
sliderBPZ1.Left = 275
sliderBPZ1.Top = 70
sliderBPZ1.Max = 100
sliderBPZ1.Min = -100
sliderBPZ2=createTrackBar(modelForm)
sliderBPZ2.Width = 125
sliderBPZ2.Height = 25
sliderBPZ2.Left = 270
sliderBPZ2.Top = 140
sliderBPZ2.Max = 100
sliderBPZ2.Min = -100
sliderBPZ3=createTrackBar(modelForm)
sliderBPZ3.Width = 125
sliderBPZ3.Height = 25
sliderBPZ3.Left = 270
sliderBPZ3.Top = 210
sliderBPZ3.Max = 100
sliderBPZ3.Min = -100
sliderBPZ4=createTrackBar(modelForm)
sliderBPZ4.Width = 125
sliderBPZ4.Height = 25
sliderBPZ4.Left = 270
sliderBPZ4.Top = 280
sliderBPZ4.Max = 100
sliderBPZ4.Min = -100
sliderBPZ5=createTrackBar(modelForm)
sliderBPZ5.Width = 125
sliderBPZ5.Height = 25
sliderBPZ5.Left = 270
sliderBPZ5.Top = 350
sliderBPZ5.Max = 100
sliderBPZ5.Min = -100
sliderBPZ6=createTrackBar(modelForm)
sliderBPZ6.Width = 125
sliderBPZ6.Height = 25
sliderBPZ6.Left = 270
sliderBPZ6.Top = 420
sliderBPZ6.Max = 100
sliderBPZ6.Min = -100
sliderBPX.Visible = false
sliderBPX2.Visible = false
sliderBPX3.Visible = false
sliderBPX4.Visible = false
sliderBPX5.Visible = false
sliderBPX6.Visible = false
sliderBPY1.Visible = false
sliderBPY2.Visible = false
sliderBPY3.Visible = false
sliderBPY4.Visible = false
sliderBPY5.Visible = false
sliderBPY6.Visible = false
sliderBPZ1.Visible = false
sliderBPZ2.Visible = false
sliderBPZ3.Visible = false
sliderBPZ4.Visible = false
sliderBPZ5.Visible = false
sliderBPZ6.Visible = false
sliderHB=createTrackBar(modelForm)
sliderHB.Width = 300
sliderHB.Height = 25
sliderHB.Left = 50
sliderHB.Top = 150
sliderHB.Max = 1000
sliderHB.Min = 0
sliderHB2=createTrackBar(modelForm)
sliderHB2.Width = 300
sliderHB2.Height = 25
sliderHB2.Left = 50
sliderHB2.Top = 250
sliderHB2.Max = 250
sliderHB2.Min = 0
sliderHB3=createTrackBar(modelForm)
sliderHB3.Width = 300
sliderHB3.Height = 25
sliderHB3.Left = 50
sliderHB3.Top = 350
sliderHB3.Max = 250
sliderHB3.Min = 0
sliderHB.Visible = false
sliderHB2.Visible = false
sliderHB3.Visible = false
MainHair=createLabel(modelForm)
MainHair.setCaption('Hair:')
MainHair.Font.Color = 0xffffff
MainHair.Font.Size = 14
MainHair.Font.Style = ('fsUnderline, fsBold')
MainHair.Top = 45
MainHair.Left = 5
MainFace=createLabel(modelForm)
MainFace.setCaption('Face:')
MainFace.Font.Color = 0xffffff
MainFace.Font.Size = 14
MainFace.Font.Style = ('fsUnderline, fsBold')
MainFace.Top = 95
MainFace.Left = 5
MainHands=createLabel(modelForm)
MainHands.setCaption('Hands:')
MainHands.Font.Color = 0xffffff
MainHands.Font.Size = 12
MainHands.Font.Style = ('fsUnderline, fsBold')
MainHands.Top = 145
MainHands.Left = 5
MainFeet=createLabel(modelForm)
MainFeet.setCaption('Feet:')
MainFeet.Font.Color = 0xffffff
MainFeet.Font.Size = 14
MainFeet.Font.Style = ('fsUnderline, fsBold')
MainFeet.Top = 195
MainFeet.Left = 5
MainChest=createLabel(modelForm)
MainChest.setCaption('Chest:')
MainChest.Font.Color = 0xffffff
MainChest.Font.Size = 14
MainChest.Font.Style = ('fsUnderline, fsBold')
MainChest.Top = 245
MainChest.Left = 5
MainShoul=createLabel(modelForm)
MainShoul.setCaption('Shoul.:')
MainShoul.Font.Color = 0xffffff
MainShoul.Font.Size = 12
MainShoul.Font.Style = ('fsUnderline, fsBold')
MainShoul.Top = 295
MainShoul.Left = 5
MainBack=createLabel(modelForm)
MainBack.setCaption('Back:')
MainBack.Font.Color = 0xffffff
MainBack.Font.Size = 14
MainBack.Font.Style = ('fsUnderline, fsBold')
MainBack.Top = 345
MainBack.Left = 5
MainWings=createLabel(modelForm)
MainWings.setCaption('Wings:')
MainWings.Font.Color = 0xffffff
MainWings.Font.Size = 12
MainWings.Font.Style = ('fsUnderline, fsBold')
MainWings.Top = 395
MainWings.Left = 5
SizeHead=createLabel(modelForm)
SizeHead.setCaption('Head:')
SizeHead.Font.Color = 0xffffff
SizeHead.Font.Size = 14
SizeHead.Font.Style = ('fsUnderline, fsBold')
SizeHead.Top = 45
SizeHead.Left = 5
SizeChest=createLabel(modelForm)
SizeChest.setCaption('Chest:')
SizeChest.Font.Color = 0xffffff
SizeChest.Font.Size = 14
SizeChest.Font.Style = ('fsUnderline, fsBold')
SizeChest.Top = 95
SizeChest.Left = 5
SizeHands=createLabel(modelForm)
SizeHands.setCaption('Hands:')
SizeHands.Font.Color = 0xffffff
SizeHands.Font.Size = 12
SizeHands.Font.Style = ('fsUnderline, fsBold')
SizeHands.Top = 145
SizeHands.Left = 5
SizeFeet=createLabel(modelForm)
SizeFeet.setCaption('Feet:')
SizeFeet.Font.Color = 0xffffff
SizeFeet.Font.Size = 14
SizeFeet.Font.Style = ('fsUnderline, fsBold')
SizeFeet.Top = 195
SizeFeet.Left = 5
SizeShoul=createLabel(modelForm)
SizeShoul.setCaption('Shoul.:')
SizeShoul.Font.Color = 0xffffff
SizeShoul.Font.Size = 12
SizeShoul.Font.Style = ('fsUnderline, fsBold')
SizeShoul.Top = 245
SizeShoul.Left = 5
SizeBack=createLabel(modelForm)
SizeBack.setCaption('Back:')
SizeBack.Font.Color = 0xffffff
SizeBack.Font.Size = 14
SizeBack.Font.Style = ('fsUnderline, fsBold')
SizeBack.Top = 295
SizeBack.Left = 5
SizeWings=createLabel(modelForm)
SizeWings.setCaption('Wings:')
SizeWings.Font.Color = 0xffffff
SizeWings.Font.Size = 12
SizeWings.Font.Style = ('fsUnderline, fsBold')
SizeWings.Top = 345
SizeWings.Left = 5
SizeWeap=createLabel(modelForm)
SizeWeap.setCaption('Weap.:')
SizeWeap.Font.Color = 0xffffff
SizeWeap.Font.Size = 12
SizeWeap.Font.Style = ('fsUnderline, fsBold')
SizeWeap.Top = 395
SizeWeap.Left = 5
SizeHead.Visible = false
SizeChest.Visible = false
SizeHands.Visible = false
SizeFeet.Visible = false
SizeShoul.Visible = false
SizeBack.Visible = false
SizeWings.Visible = false
SizeWeap.Visible = false
RotationChestZY=createLabel(modelForm)
RotationChestZY.setCaption('ChestZY:')
RotationChestZY.Font.Color = 0xffffff
RotationChestZY.Font.Size = 10
RotationChestZY.Font.Style = ('fsUnderline, fsBold')
RotationChestZY.Top = 100
RotationChestZY.Left = 4
RotationHandsZY=createLabel(modelForm)
RotationHandsZY.setCaption('HandZY:')
RotationHandsZY.Font.Color = 0xffffff
RotationHandsZY.Font.Size = 10
RotationHandsZY.Font.Style = ('fsUnderline, fsBold')
RotationHandsZY.Top = 150
RotationHandsZY.Left = 4
RotationHandsXY=createLabel(modelForm)
RotationHandsXY.setCaption('HandXY:')
RotationHandsXY.Font.Color = 0xffffff
RotationHandsXY.Font.Size = 10
RotationHandsXY.Font.Style = ('fsUnderline, fsBold')
RotationHandsXY.Top = 200
RotationHandsXY.Left = 4
RotationHandsZX=createLabel(modelForm)
RotationHandsZX.setCaption('HandZX:')
RotationHandsZX.Font.Color = 0xffffff
RotationHandsZX.Font.Size = 10
RotationHandsZX.Font.Style = ('fsUnderline, fsBold')
RotationHandsZX.Top = 250
RotationHandsZX.Left = 4
RotationFeetZY=createLabel(modelForm)
RotationFeetZY.setCaption('FeetZY:')
RotationFeetZY.Font.Color = 0xffffff
RotationFeetZY.Font.Size = 10
RotationFeetZY.Font.Style = ('fsUnderline, fsBold')
RotationFeetZY.Top = 300
RotationFeetZY.Left = 5
RotationWingsZY=createLabel(modelForm)
RotationWingsZY.setCaption('WingZY:')
RotationWingsZY.Font.Color = 0xffffff
RotationWingsZY.Font.Size = 10
RotationWingsZY.Font.Style = ('fsUnderline, fsBold')
RotationWingsZY.Top = 350
RotationWingsZY.Left = 4
RotationBackZY=createLabel(modelForm)
RotationBackZY.setCaption('BackZY:')
RotationBackZY.Font.Color = 0xffffff
RotationBackZY.Font.Size = 10
RotationBackZY.Font.Style = ('fsUnderline, fsBold')
RotationBackZY.Top = 400
RotationBackZY.Left = 5
RotationChestZY.Visible = false
RotationHandsZY.Visible = false
RotationHandsXY.Visible = false
RotationHandsZX.Visible = false
RotationFeetZY.Visible = false
RotationWingsZY.Visible = false
RotationBackZY.Visible = false
PositionCentralBody=createLabel(modelForm)
PositionCentralBody.setCaption('CentralBody:')
PositionCentralBody.Font.Color = 0xffffff
PositionCentralBody.Font.Size = 12
PositionCentralBody.Font.Style = ('fsUnderline, fsBold')
PositionCentralBody.Top = 30
PositionCentralBody.Left = 152
PositionHead=createLabel(modelForm)
PositionHead.setCaption('Head:')
PositionHead.Font.Color = 0xffffff
PositionHead.Font.Size = 12
PositionHead.Font.Style = ('fsUnderline, fsBold')
PositionHead.Top = 100
PositionHead.Left = 181
PositionHands=createLabel(modelForm)
PositionHands.setCaption('Hands:')
PositionHands.Font.Color = 0xffffff
PositionHands.Font.Size = 12
PositionHands.Font.Style = ('fsUnderline, fsBold')
PositionHands.Top = 170
PositionHands.Left = 177
PositionFeet=createLabel(modelForm)
PositionFeet.setCaption('Feet:')
PositionFeet.Font.Color = 0xffffff
PositionFeet.Font.Size = 12
PositionFeet.Font.Style = ('fsUnderline, fsBold')
PositionFeet.Top = 240
PositionFeet.Left = 185
PositionWings=createLabel(modelForm)
PositionWings.setCaption('Wings:')
PositionWings.Font.Color = 0xffffff
PositionWings.Font.Size = 12
PositionWings.Font.Style = ('fsUnderline, fsBold')
PositionWings.Top = 310
PositionWings.Left = 177
PositionBack=createLabel(modelForm)
PositionBack.setCaption('Back:')
PositionBack.Font.Color = 0xffffff
PositionBack.Font.Size = 12
PositionBack.Font.Style = ('fsUnderline, fsBold')
PositionBack.Top = 380
PositionBack.Left = 182
PositionCentralBody.Visible = false
PositionHead.Visible = false
PositionHands.Visible = false
PositionFeet.Visible = false
PositionWings.Visible = false
PositionBack.Visible = false
PositionCentralBodyx=createLabel(modelForm)
PositionCentralBodyx.setCaption('X:')
PositionCentralBodyx.Font.Color = 0xffffff
PositionCentralBodyx.Font.Size = 8
PositionCentralBodyx.Font.Style = ('fsBold')
PositionCentralBodyx.Top = 75
PositionCentralBodyx.Left = 5
PositionHeadx=createLabel(modelForm)
PositionHeadx.setCaption('X:')
PositionHeadx.Font.Color = 0xffffff
PositionHeadx.Font.Size = 8
PositionHeadx.Font.Style = ('fsBold')
PositionHeadx.Top = 145
PositionHeadx.Left = 5
PositionHandsx=createLabel(modelForm)
PositionHandsx.setCaption('X:')
PositionHandsx.Font.Color = 0xffffff
PositionHandsx.Font.Size = 8
PositionHandsx.Font.Style = ('fsBold')
PositionHandsx.Top = 215
PositionHandsx.Left = 5
PositionFeetx=createLabel(modelForm)
PositionFeetx.setCaption('X:')
PositionFeetx.Font.Color = 0xffffff
PositionFeetx.Font.Size = 8
PositionFeetx.Font.Style = ('fsBold')
PositionFeetx.Top = 285
PositionFeetx.Left = 5
PositionWingsx=createLabel(modelForm)
PositionWingsx.setCaption('X:')
PositionWingsx.Font.Color = 0xffffff
PositionWingsx.Font.Size = 8
PositionWingsx.Font.Style = ('fsBold')
PositionWingsx.Top = 355
PositionWingsx.Left = 5
PositionBackx=createLabel(modelForm)
PositionBackx.setCaption('X:')
PositionBackx.Font.Color = 0xffffff
PositionBackx.Font.Size = 8
PositionBackx.Font.Style = ('fsBold')
PositionBackx.Top = 425
PositionBackx.Left = 5
PositionCentralBodyx.Visible = false
PositionHeadx.Visible = false
PositionHandsx.Visible = false
PositionFeetx.Visible = false
PositionWingsx.Visible = false
PositionBackx.Visible = false
PositionCentralBodyy=createLabel(modelForm)
PositionCentralBodyy.setCaption('Y:')
PositionCentralBodyy.Font.Color = 0xffffff
PositionCentralBodyy.Font.Size = 8
PositionCentralBodyy.Font.Style = ('fsBold')
PositionCentralBodyy.Top = 75
PositionCentralBodyy.Left = 135
PositionHeady=createLabel(modelForm)
PositionHeady.setCaption('Y:')
PositionHeady.Font.Color = 0xffffff
PositionHeady.Font.Size = 8
PositionHeady.Font.Style = ('fsBold')
PositionHeady.Top = 145
PositionHeady.Left = 135
PositionHandsy=createLabel(modelForm)
PositionHandsy.setCaption('Y:')
PositionHandsy.Font.Color = 0xffffff
PositionHandsy.Font.Size = 8
PositionHandsy.Font.Style = ('fsBold')
PositionHandsy.Top = 215
PositionHandsy.Left = 135
PositionFeety=createLabel(modelForm)
PositionFeety.setCaption('Y')
PositionFeety.Font.Color = 0xffffff
PositionFeety.Font.Size = 8
PositionFeety.Font.Style = ('fsBold')
PositionFeety.Top = 285
PositionFeety.Left = 135
PositionWingsy=createLabel(modelForm)
PositionWingsy.setCaption('Y:')
PositionWingsy.Font.Color = 0xffffff
PositionWingsy.Font.Size = 8
PositionWingsy.Font.Style = ('fsBold')
PositionWingsy.Top = 355
PositionWingsy.Left = 135
PositionBacky=createLabel(modelForm)
PositionBacky.setCaption('Y:')
PositionBacky.Font.Color = 0xffffff
PositionBacky.Font.Size = 8
PositionBacky.Font.Style = ('fsBold')
PositionBacky.Top = 425
PositionBacky.Left = 135
PositionCentralBodyy.Visible = false
PositionHeady.Visible = false
PositionHandsy.Visible = false
PositionFeety.Visible = false
PositionWingsy.Visible = false
PositionBacky.Visible = false
PositionCentralBodyz=createLabel(modelForm)
PositionCentralBodyz.setCaption('Z:')
PositionCentralBodyz.Font.Color = 0xffffff
PositionCentralBodyz.Font.Size = 8
PositionCentralBodyz.Font.Style = ('fsBold')
PositionCentralBodyz.Top = 75
PositionCentralBodyz.Left = 265
PositionHeadz=createLabel(modelForm)
PositionHeadz.setCaption('Z:')
PositionHeadz.Font.Color = 0xffffff
PositionHeadz.Font.Size = 8
PositionHeadz.Font.Style = ('fsBold')
PositionHeadz.Top = 150
PositionHeadz.Left = 265
PositionHandsz=createLabel(modelForm)
PositionHandsz.setCaption('Z:')
PositionHandsz.Font.Color = 0xffffff
PositionHandsz.Font.Size = 8
PositionHandsz.Font.Style = ('fsBold')
PositionHandsz.Top = 225
PositionHandsz.Left = 265
PositionFeetz=createLabel(modelForm)
PositionFeetz.setCaption('Z:')
PositionFeetz.Font.Color = 0xffffff
PositionFeetz.Font.Size = 8
PositionFeetz.Font.Style = ('fsBold')
PositionFeetz.Top = 300
PositionFeetz.Left = 265
PositionWingsz=createLabel(modelForm)
PositionWingsz.setCaption('Z:')
PositionWingsz.Font.Color = 0xffffff
PositionWingsz.Font.Size = 8
PositionWingsz.Font.Style = ('fsBold')
PositionWingsz.Top = 375
PositionWingsz.Left = 265
PositionBackz=createLabel(modelForm)
PositionBackz.setCaption('Z:')
PositionBackz.Font.Color = 0xffffff
PositionBackz.Font.Size = 8
PositionBackz.Font.Style = ('fsBold')
PositionBackz.Top = 425
PositionBackz.Left = 265
PositionCentralBodyz.Visible = false
PositionHeadz.Visible = false
PositionHandsz.Visible = false
PositionFeetz.Visible = false
PositionWingsz.Visible = false
PositionBackz.Visible = false
HBHeight=createLabel(modelForm)
HBHeight.setCaption('Height:')
HBHeight.Font.Color = 0xffffff
HBHeight.Font.Size = 12
HBHeight.Font.Style = ('fsUnderline, fsBold')
HBHeight.Top = 125
HBHeight.Left = 170
HBScaleHeight=createLabel(modelForm)
HBScaleHeight.setCaption('Scale Height:')
HBScaleHeight.Font.Color = 0xffffff
HBScaleHeight.Font.Size = 12
HBScaleHeight.Font.Style = ('fsUnderline, fsBold')
HBScaleHeight.Top = 225
HBScaleHeight.Left = 150
HBScaleWidth=createLabel(modelForm)
HBScaleWidth.setCaption('Scale Width:')
HBScaleWidth.Font.Color = 0xffffff
HBScaleWidth.Font.Size = 12
HBScaleWidth.Font.Style = ('fsUnderline, fsBold')
HBScaleWidth.Top = 325
HBScaleWidth.Left = 150
HBHeight.Visible = false
HBScaleHeight.Visible = false
HBScaleWidth.Visible = false
--Actual Value Send/Get--
slider.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92", getProperty(slider, 'Position'))
end
sliderRefreshTimer = createTimer(getMainForm())
sliderRefreshTimer.Interval = 500
sliderRefreshTimer.onTimer = function(sender)
  if slider.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92") then
  else
  setProperty(slider, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92"))
 end
end
slider2.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90", getProperty(slider2, 'Position'))
end
slider2RefreshTimer = createTimer(getMainForm())
slider2RefreshTimer.Interval = 500
slider2RefreshTimer.onTimer = function(sender)
  if slider2.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90") then
  else
  setProperty(slider2, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90"))
 end
end
slider3.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94", getProperty(slider3, 'Position'))
end
slider3RefreshTimer = createTimer(getMainForm())
slider3RefreshTimer.Interval = 500
slider3RefreshTimer.onTimer = function(sender)
  if slider3.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94") then
  else
  setProperty(slider3, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94"))
 end
end
slider4.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96", getProperty(slider4, 'Position'))
end
slider4RefreshTimer = createTimer(getMainForm())
slider4RefreshTimer.Interval = 500
slider4RefreshTimer.onTimer = function(sender)
  if slider4.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96") then
  else
  setProperty(slider4, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96"))
 end
end
slider5.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+98", getProperty(slider5, 'Position'))
end
slider5RefreshTimer = createTimer(getMainForm())
slider5RefreshTimer.Interval = 500
slider5RefreshTimer.onTimer = function(sender)
  if slider5.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+98") then
  else
  setProperty(slider5, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+98"))
 end
end
slider6.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C", getProperty(slider6, 'Position'))
end
slider6RefreshTimer = createTimer(getMainForm())
slider6RefreshTimer.Interval = 500
slider6RefreshTimer.onTimer = function(sender)
  if slider6.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C") then
  else
  setProperty(slider6, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C"))
 end
end
slider7.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A", getProperty(slider7, 'Position'))
end
slider7RefreshTimer = createTimer(getMainForm())
slider7RefreshTimer.Interval = 500
slider7RefreshTimer.onTimer = function(sender)
  if slider7.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A") then
  else
  setProperty(slider7, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A"))
 end
end
slider8.OnChange = function (sender)
writeSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E", getProperty(slider8, 'Position'))
end
slider8RefreshTimer = createTimer(getMainForm())
slider8RefreshTimer.Interval = 500
slider8RefreshTimer.onTimer = function(sender)
  if slider8.position == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E") then
  else
  setProperty(slider8, 'Position', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E"))
 end
end
sliderBS.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A0", getProperty(sliderBS, 'Position')*0.01)
end
sliderBSRefreshTimer = createTimer(getMainForm())
sliderBSRefreshTimer.Interval = 1500
sliderBSRefreshTimer.onTimer = function(sender)
  if (sliderBS.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A0") then
  elseif tonumber(BSedit.Text) ~= nil then
  setProperty(sliderBS, 'Position', (round(tonumber(BSedit.Text)/0.01)))
 end
end
sliderBS2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A4", getProperty(sliderBS2, 'Position')*0.01)
end
sliderBS2RefreshTimer = createTimer(getMainForm())
sliderBS2RefreshTimer.Interval = 1500
sliderBS2RefreshTimer.onTimer = function(sender)
  if (sliderBS2.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A4") then
  elseif tonumber(BSedit2.Text) ~= nil then
  setProperty(sliderBS2, 'Position', (round(tonumber(BSedit2.Text)/0.01)))
 end
end
sliderBS3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A8", getProperty(sliderBS3, 'Position')*0.01)
end
sliderBS3RefreshTimer = createTimer(getMainForm())
sliderBS3RefreshTimer.Interval = 1500
sliderBS3RefreshTimer.onTimer = function(sender)
  if (sliderBS3.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A8") then
  elseif tonumber(BSedit3.Text) ~= nil then
  setProperty(sliderBS3, 'Position', (round(tonumber(BSedit3.Text)/0.01)))
 end
end
sliderBS4.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AC", getProperty(sliderBS4, 'Position')*0.01)
end
sliderBS4RefreshTimer = createTimer(getMainForm())
sliderBS4RefreshTimer.Interval = 1500
sliderBS4RefreshTimer.onTimer = function(sender)
  if (sliderBS4.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AC") then
  elseif tonumber(BSedit4.Text) ~= nil then
  setProperty(sliderBS4, 'Position', (round(tonumber(BSedit4.Text)/0.01)))
 end
end
sliderBS5.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B0", getProperty(sliderBS5, 'Position')*0.01)
end
sliderBS5RefreshTimer = createTimer(getMainForm())
sliderBS5RefreshTimer.Interval = 1500
sliderBS5RefreshTimer.onTimer = function(sender)
  if (sliderBS5.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B0") then
  elseif tonumber(BSedit5.Text) ~= nil then
  setProperty(sliderBS5, 'Position', (round(tonumber(BSedit5.Text)/0.01)))
 end
end
sliderBS6.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B8", getProperty(sliderBS6, 'Position')*0.01)
end
sliderBS6RefreshTimer = createTimer(getMainForm())
sliderBS6RefreshTimer.Interval = 1500
sliderBS6RefreshTimer.onTimer = function(sender)
  if (sliderBS6.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B8") then
  elseif tonumber(BSedit6.Text) ~= nil then
  setProperty(sliderBS6, 'Position', (round(tonumber(BSedit6.Text)/0.01)))
 end
end
sliderBS7.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C0", getProperty(sliderBS7, 'Position')*0.01)
end
sliderBS7RefreshTimer = createTimer(getMainForm())
sliderBS7RefreshTimer.Interval = 1500
sliderBS7RefreshTimer.onTimer = function(sender)
  if (sliderBS7.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C0") then
  elseif tonumber(BSedit7.Text) ~= nil then
  setProperty(sliderBS7, 'Position', (round(tonumber(BSedit7.Text)/0.01)))
 end
end
sliderBS8.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B4", getProperty(sliderBS8, 'Position')*0.01)
end
sliderBS8RefreshTimer = createTimer(getMainForm())
sliderBS8RefreshTimer.Interval = 1500
sliderBS8RefreshTimer.onTimer = function(sender)
  if (sliderBS8.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B4") then
  elseif tonumber(BSedit8.Text) ~= nil then
  setProperty(sliderBS8, 'Position', (round(tonumber(BSedit8.Text)/0.01)))
 end
end
sliderBR2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C4", getProperty(sliderBR2, 'Position'))
end
sliderBR2RefreshTimer = createTimer(getMainForm())
sliderBR2RefreshTimer.Interval = 500
sliderBR2RefreshTimer.onTimer = function(sender)
  if sliderBR2.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C4") then
  else
  setProperty(sliderBR2, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C4"))
 end
end
sliderBR3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C8", getProperty(sliderBR3, 'Position'))
end
sliderBR3RefreshTimer = createTimer(getMainForm())
sliderBR3RefreshTimer.Interval = 500
sliderBR3RefreshTimer.onTimer = function(sender)
  if sliderBR3.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C8") then
  else
  setProperty(sliderBR3, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C8"))
 end
end
sliderBR4.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+CC", getProperty(sliderBR4, 'Position'))
end
sliderBR4RefreshTimer = createTimer(getMainForm())
sliderBR4RefreshTimer.Interval = 500
sliderBR4RefreshTimer.onTimer = function(sender)
  if sliderBR4.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+CC") then
  else
  setProperty(sliderBR4, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+CC"))
 end
end
sliderBR5.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D0", getProperty(sliderBR5, 'Position'))
end
sliderBR5RefreshTimer = createTimer(getMainForm())
sliderBR5RefreshTimer.Interval = 500
sliderBR5RefreshTimer.onTimer = function(sender)
  if sliderBR5.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D0") then
  else
  setProperty(sliderBR5, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D0"))
 end
end
sliderBR6.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D4", getProperty(sliderBR6, 'Position'))
end
sliderBR6RefreshTimer = createTimer(getMainForm())
sliderBR6RefreshTimer.Interval = 500
sliderBR6RefreshTimer.onTimer = function(sender)
  if sliderBR6.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D4") then
  else
  setProperty(sliderBR6, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D4"))
 end
end
sliderBR7.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D8", getProperty(sliderBR7, 'Position'))
end
sliderBR7RefreshTimer = createTimer(getMainForm())
sliderBR7RefreshTimer.Interval = 500
sliderBR7RefreshTimer.onTimer = function(sender)
  if sliderBR7.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D8") then
  else
  setProperty(sliderBR7, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D8"))
 end
end
sliderBR8.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+DC", getProperty(sliderBR8, 'Position'))
end
sliderBR8RefreshTimer = createTimer(getMainForm())
sliderBR8RefreshTimer.Interval = 500
sliderBR8RefreshTimer.onTimer = function(sender)
  if sliderBR8.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+DC") then
  else
  setProperty(sliderBR8, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+DC"))
 end
end
sliderBPX.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E0", getProperty(sliderBPX, 'Position'))
end
sliderBPXRefreshTimer = createTimer(getMainForm())
sliderBPXRefreshTimer.Interval = 500
sliderBPXRefreshTimer.onTimer = function(sender)
  if sliderBPX.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E0") then
  else
  setProperty(sliderBPX, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E0"))
 end
end
sliderBPX2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+EC", getProperty(sliderBPX2, 'Position'))
end
sliderBPX2RefreshTimer = createTimer(getMainForm())
sliderBPX2RefreshTimer.Interval = 500
sliderBPX2RefreshTimer.onTimer = function(sender)
  if sliderBPX2.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+EC") then
  else
  setProperty(sliderBPX2, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+EC"))
 end
end
sliderBPX3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F8", getProperty(sliderBPX3, 'Position'))
end
sliderBPX3RefreshTimer = createTimer(getMainForm())
sliderBPX3RefreshTimer.Interval = 500
sliderBPX3RefreshTimer.onTimer = function(sender)
  if sliderBPX3.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F8") then
  else
  setProperty(sliderBPX3, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F8"))
 end
end
sliderBPX4.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+104", getProperty(sliderBPX4, 'Position'))
end
sliderBPX4RefreshTimer = createTimer(getMainForm())
sliderBPX4RefreshTimer.Interval = 500
sliderBPX4RefreshTimer.onTimer = function(sender)
  if sliderBPX4.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+104") then
  else
  setProperty(sliderBPX4, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+104"))
 end
end
sliderBPX5.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+11C", getProperty(sliderBPX5, 'Position'))
end
sliderBPX5RefreshTimer = createTimer(getMainForm())
sliderBPX5RefreshTimer.Interval = 500
sliderBPX5RefreshTimer.onTimer = function(sender)
  if sliderBPX5.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+11C") then
  else
  setProperty(sliderBPX5, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+11C"))
 end
end
sliderBPX6.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+110", getProperty(sliderBPX6, 'Position'))
end
sliderBPX6RefreshTimer = createTimer(getMainForm())
sliderBPX6RefreshTimer.Interval = 500
sliderBPX6RefreshTimer.onTimer = function(sender)
  if sliderBPX6.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+110") then
  else
  setProperty(sliderBPX6, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+110"))
 end
end
sliderBPY1.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E8", getProperty(sliderBPY1, 'Position'))
end
sliderBPY1RefreshTimer = createTimer(getMainForm())
sliderBPY1RefreshTimer.Interval = 500
sliderBPY1RefreshTimer.onTimer = function(sender)
  if sliderBPY1.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E8") then
  else
  setProperty(sliderBPY1, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E8"))
 end
end
sliderBPY2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F4", getProperty(sliderBPY2, 'Position'))
end
sliderBPY2RefreshTimer = createTimer(getMainForm())
sliderBPY2RefreshTimer.Interval = 500
sliderBPY2RefreshTimer.onTimer = function(sender)
  if sliderBPY2.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F4") then
  else
  setProperty(sliderBPY2, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F4"))
 end
end
sliderBPY3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+100", getProperty(sliderBPY3, 'Position'))
end
sliderBPY3RefreshTimer = createTimer(getMainForm())
sliderBPY3RefreshTimer.Interval = 500
sliderBPY3RefreshTimer.onTimer = function(sender)
  if sliderBPY3.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+100") then
  else
  setProperty(sliderBPY3, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+100"))
 end
end
sliderBPY4.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+10C", getProperty(sliderBPY4, 'Position'))
end
sliderBPY4RefreshTimer = createTimer(getMainForm())
sliderBPY4RefreshTimer.Interval = 500
sliderBPY4RefreshTimer.onTimer = function(sender)
  if sliderBPY4.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+10C") then
  else
  setProperty(sliderBPY4, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+10C"))
 end
end
sliderBPY5.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+124", getProperty(sliderBPY5, 'Position'))
end
sliderBPY5RefreshTimer = createTimer(getMainForm())
sliderBPY5RefreshTimer.Interval = 500
sliderBPY5RefreshTimer.onTimer = function(sender)
  if sliderBPY5.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+124") then
  else
  setProperty(sliderBPY5, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+124"))
 end
end
sliderBPY6.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+118", getProperty(sliderBPY6, 'Position'))
end
sliderBPY6RefreshTimer = createTimer(getMainForm())
sliderBPY6RefreshTimer.Interval = 500
sliderBPY6RefreshTimer.onTimer = function(sender)
  if sliderBPY6.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+118") then
  else
  setProperty(sliderBPY6, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+118"))
 end
end
sliderBPZ1.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E4", getProperty(sliderBPZ1, 'Position'))
end
sliderBPZ1RefreshTimer = createTimer(getMainForm())
sliderBPZ1RefreshTimer.Interval = 500
sliderBPZ1RefreshTimer.onTimer = function(sender)
  if sliderBPZ1.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E4") then
  else
  setProperty(sliderBPZ1, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E4"))
 end
end
sliderBPZ2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F0", getProperty(sliderBPZ2, 'Position'))
end
sliderBPZ2RefreshTimer = createTimer(getMainForm())
sliderBPZ2RefreshTimer.Interval = 500
sliderBPZ2RefreshTimer.onTimer = function(sender)
  if sliderBPZ2.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F0") then
  else
  setProperty(sliderBPZ2, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F0"))
 end
end
sliderBPZ3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+FC", getProperty(sliderBPZ3, 'Position'))
end
sliderBPZ3RefreshTimer = createTimer(getMainForm())
sliderBPZ3RefreshTimer.Interval = 500
sliderBPZ3RefreshTimer.onTimer = function(sender)
  if sliderBPZ3.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+FC") then
  else
  setProperty(sliderBPZ3, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+FC"))
 end
end
sliderBPZ4.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+108", getProperty(sliderBPZ4, 'Position'))
end
sliderBPZ4RefreshTimer = createTimer(getMainForm())
sliderBPZ4RefreshTimer.Interval = 500
sliderBPZ4RefreshTimer.onTimer = function(sender)
  if sliderBPZ4.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+108") then
  else
  setProperty(sliderBPZ4, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+108"))
 end
end
sliderBPZ5.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+120", getProperty(sliderBPZ5, 'Position'))
end
sliderBPZ5RefreshTimer = createTimer(getMainForm())
sliderBPZ5RefreshTimer.Interval = 500
sliderBPZ5RefreshTimer.onTimer = function(sender)
  if sliderBPZ5.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+120") then
  else
  setProperty(sliderBPZ5, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+120"))
 end
end
sliderBPZ6.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+114", getProperty(sliderBPZ6, 'Position'))
end
sliderBPZ6RefreshTimer = createTimer(getMainForm())
sliderBPZ6RefreshTimer.Interval = 500
sliderBPZ6RefreshTimer.onTimer = function(sender)
  if sliderBPZ6.position == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+114") then
  else
  setProperty(sliderBPZ6, 'Position', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+114"))
 end
end
sliderHB.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8C", getProperty(sliderHB, 'Position')*0.01)
end
sliderHBRefreshTimer = createTimer(getMainForm())
sliderHBRefreshTimer.Interval = 5000
sliderHBRefreshTimer.onTimer = function(sender)
  if (sliderHB.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8C") then
  elseif tonumber(HBedit.Text) ~= nil then
  setProperty(sliderHB, 'Position', (round(tonumber(HBedit.Text)/0.01)))
 end
end
sliderHB2.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+88", getProperty(sliderHB2, 'Position')*0.01)
end
sliderHB2RefreshTimer = createTimer(getMainForm())
sliderHB2RefreshTimer.Interval = 5000
sliderHB2RefreshTimer.onTimer = function(sender)
  if (sliderHB2.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+88") then
  elseif tonumber(HBedit2.Text) ~= nil then
  setProperty(sliderHB2, 'Position', (round(tonumber(HBedit2.Text)/0.01)))
 end
end
sliderHB3.OnChange = function (sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+84", getProperty(sliderHB3, 'Position')*0.01)
end
sliderHB3RefreshTimer = createTimer(getMainForm())
sliderHB3RefreshTimer.Interval = 5000
sliderHB3RefreshTimer.onTimer = function(sender)
  if (sliderHB3.position*0.01) == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+84") then
  elseif tonumber(HBedit3.Text) ~= nil then
  setProperty(sliderHB3, 'Position', (round(tonumber(HBedit3.Text)/0.01)))
 end
end

modelForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox5, 0)
   return caHide
end
function UDF1_CEToggleBox5Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox5) == 1) then
modelForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox5) == 0) then
modelForm.hide()
  end
end
Mainedit=createEdit(modelForm)
Mainedit.Top = 50
Mainedit.Left = 350
Mainedit.Width = 40
MaineditRefreshTimer1 = createTimer(getMainForm())
MaineditRefreshTimer1.Interval = 500
MaineditRefreshTimer1.onTimer = function(sender)
  if Mainedit.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92") then
  else
  setProperty(Mainedit, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+92"))
 end
end
Mainedit2=createEdit(modelForm)
Mainedit2.Top = 100
Mainedit2.Left = 350
Mainedit2.Width = 40
MaineditRefreshTimer2 = createTimer(getMainForm())
MaineditRefreshTimer2.Interval = 500
MaineditRefreshTimer2.onTimer = function(sender)
  if Mainedit2.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90") then
  else
  setProperty(Mainedit2, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+90"))
 end
end
Mainedit3=createEdit(modelForm)
Mainedit3.Top = 150
Mainedit3.Left = 350
Mainedit3.Width = 40
MaineditRefreshTimer3 = createTimer(getMainForm())
MaineditRefreshTimer3.Interval = 500
MaineditRefreshTimer3.onTimer = function(sender)
  if Mainedit3.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94") then
  else
  setProperty(Mainedit3, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+94"))
 end
end
Mainedit4=createEdit(modelForm)
Mainedit4.Top = 200
Mainedit4.Left = 350
Mainedit4.Width = 40
MaineditRefreshTimer4 = createTimer(getMainForm())
MaineditRefreshTimer4.Interval = 500
MaineditRefreshTimer4.onTimer = function(sender)
  if Mainedit4.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96") then
  else
  setProperty(Mainedit4, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+96"))
 end
end
Mainedit5=createEdit(modelForm)
Mainedit5.Top = 250
Mainedit5.Left = 350
Mainedit5.Width = 40
MaineditRefreshTimer5 = createTimer(getMainForm())
MaineditRefreshTimer5.Interval = 500
MaineditRefreshTimer5.onTimer = function(sender)
  if Mainedit5.text == readSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98") then
  else
  setProperty(Mainedit5, 'text', readSmallInteger("[[[[cubeworld.exe+00551E80]+2E0]+1E8]+248]+98"))
 end
end
Mainedit6=createEdit(modelForm)
Mainedit6.Top = 300
Mainedit6.Left = 350
Mainedit6.Width = 40
MaineditRefreshTimer6 = createTimer(getMainForm())
MaineditRefreshTimer6.Interval = 500
MaineditRefreshTimer6.onTimer = function(sender)
  if Mainedit6.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C") then
  else
  setProperty(Mainedit6, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9C"))
 end
end
Mainedit7=createEdit(modelForm)
Mainedit7.Top = 350
Mainedit7.Left = 350
Mainedit7.Width = 40
MaineditRefreshTimer7 = createTimer(getMainForm())
MaineditRefreshTimer7.Interval = 500
MaineditRefreshTimer7.onTimer = function(sender)
  if Mainedit7.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A") then
  else
  setProperty(Mainedit7, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A"))
 end
end
Mainedit8=createEdit(modelForm)
Mainedit8.Top = 400
Mainedit8.Left = 350
Mainedit8.Width = 40
MaineditRefreshTimer8 = createTimer(getMainForm())
MaineditRefreshTimer8.Interval = 500
MaineditRefreshTimer8.onTimer = function(sender)
  if Mainedit8.text == readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E") then
  else
  setProperty(Mainedit8, 'text', readSmallInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9E"))
 end
end
BSedit=createEdit(modelForm)
BSedit.Top = 50
BSedit.Left = 350
BSedit.Width = 40
BSeditRefreshTimer = createTimer(getMainForm())
BSeditRefreshTimer.Interval = 500
BSeditRefreshTimer.onTimer = function(sender)
  if BSedit.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A0") then
  else
  setProperty(BSedit, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A0"))
 end
end
BSedit2=createEdit(modelForm)
BSedit2.Top = 100
BSedit2.Left = 350
BSedit2.Width = 40
BSeditRefreshTimer2 = createTimer(getMainForm())
BSeditRefreshTimer2.Interval = 500
BSeditRefreshTimer2.onTimer = function(sender)
  if BSedit2.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A4") then
  else
  setProperty(BSedit2, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A4"))
 end
end
BSedit3=createEdit(modelForm)
BSedit3.Top = 150
BSedit3.Left = 350
BSedit3.Width = 40
BSeditRefreshTimer3 = createTimer(getMainForm())
BSeditRefreshTimer3.Interval = 500
BSeditRefreshTimer3.onTimer = function(sender)
  if BSedit3.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A8") then
  else
  setProperty(BSedit3, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+A8"))
 end
end
BSedit4=createEdit(modelForm)
BSedit4.Top = 200
BSedit4.Left = 350
BSedit4.Width = 40
BSeditRefreshTimer4 = createTimer(getMainForm())
BSeditRefreshTimer4.Interval = 500
BSeditRefreshTimer4.onTimer = function(sender)
  if BSedit4.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AC") then
  else
  setProperty(BSedit4, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AC"))
 end
end
BSedit5=createEdit(modelForm)
BSedit5.Top = 250
BSedit5.Left = 350
BSedit5.Width = 40
BSeditRefreshTimer5 = createTimer(getMainForm())
BSeditRefreshTimer5.Interval = 500
BSeditRefreshTimer5.onTimer = function(sender)
  if BSedit5.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B0") then
  else
  setProperty(BSedit5, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B0"))
 end
end
BSedit6=createEdit(modelForm)
BSedit6.Top = 300
BSedit6.Left = 350
BSedit6.Width = 40
BSeditRefreshTimer6 = createTimer(getMainForm())
BSeditRefreshTimer6.Interval = 500
BSeditRefreshTimer6.onTimer = function(sender)
  if BSedit6.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B8") then
  else
  setProperty(BSedit6, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B8"))
 end
end
BSedit7=createEdit(modelForm)
BSedit7.Top = 350
BSedit7.Left = 350
BSedit7.Width = 40
BSeditRefreshTimer7 = createTimer(getMainForm())
BSeditRefreshTimer7.Interval = 500
BSeditRefreshTimer7.onTimer = function(sender)
  if BSedit7.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C0") then
  else
  setProperty(BSedit7, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C0"))
 end
end
BSedit8=createEdit(modelForm)
BSedit8.Top = 400
BSedit8.Left = 350
BSedit8.Width = 40
BSeditRefreshTimer8 = createTimer(getMainForm())
BSeditRefreshTimer8.Interval = 500
BSeditRefreshTimer8.onTimer = function(sender)
  if BSedit8.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B4") then
  else
  setProperty(BSedit8, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+B4"))
 end
end
BSedit.Visible = false
BSedit2.Visible = false
BSedit3.Visible = false
BSedit4.Visible = false
BSedit5.Visible = false
BSedit6.Visible = false
BSedit7.Visible = false
BSedit8.Visible = false
BRedit2=createEdit(modelForm)
BRedit2.Top = 100
BRedit2.Left = 350
BRedit2.Width = 40
BReditRefreshTimer2 = createTimer(getMainForm())
BReditRefreshTimer2.Interval = 500
BReditRefreshTimer2.onTimer = function(sender)
  if BRedit2.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C4") then
  else
  setProperty(BRedit2, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C4"))
 end
end
BRedit3=createEdit(modelForm)
BRedit3.Top = 150
BRedit3.Left = 350
BRedit3.Width = 40
BReditRefreshTimer3 = createTimer(getMainForm())
BReditRefreshTimer3.Interval = 500
BReditRefreshTimer3.onTimer = function(sender)
  if BRedit3.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C8") then
  else
  setProperty(BRedit3, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+C8"))
 end
end
BRedit4=createEdit(modelForm)
BRedit4.Top = 200
BRedit4.Left = 350
BRedit4.Width = 40
BReditRefreshTimer4 = createTimer(getMainForm())
BReditRefreshTimer4.Interval = 500
BReditRefreshTimer4.onTimer = function(sender)
  if BRedit4.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+CC") then
  else
  setProperty(BRedit4, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+CC"))
 end
end
BRedit5=createEdit(modelForm)
BRedit5.Top = 250
BRedit5.Left = 350
BRedit5.Width = 40
BReditRefreshTimer5 = createTimer(getMainForm())
BReditRefreshTimer5.Interval = 500
BReditRefreshTimer5.onTimer = function(sender)
  if BRedit5.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D0") then
  else
  setProperty(BRedit5, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D0"))
 end
end
BRedit6=createEdit(modelForm)
BRedit6.Top = 300
BRedit6.Left = 350
BRedit6.Width = 40
BReditRefreshTimer6 = createTimer(getMainForm())
BReditRefreshTimer6.Interval = 500
BReditRefreshTimer6.onTimer = function(sender)
  if BRedit6.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D4") then
  else
  setProperty(BRedit6, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D4"))
 end
end
BRedit7=createEdit(modelForm)
BRedit7.Top = 350
BRedit7.Left = 350
BRedit7.Width = 40
BReditRefreshTimer7 = createTimer(getMainForm())
BReditRefreshTimer7.Interval = 500
BReditRefreshTimer7.onTimer = function(sender)
  if BRedit7.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D8") then
  else
  setProperty(BRedit7, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+D8"))
 end
end
BRedit8=createEdit(modelForm)
BRedit8.Top = 400
BRedit8.Left = 350
BRedit8.Width = 40
BReditRefreshTimer8 = createTimer(getMainForm())
BReditRefreshTimer8.Interval = 500
BReditRefreshTimer8.onTimer = function(sender)
  if BRedit8.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+DC") then
  else
  setProperty(BRedit8, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+DC"))
 end
end
BRedit2.Visible = false
BRedit3.Visible = false
BRedit4.Visible = false
BRedit5.Visible = false
BRedit6.Visible = false
BRedit7.Visible = false
BRedit8.Visible = false
BPeditX2=createEdit(modelForm)
BPeditX2.Top = 50
BPeditX2.Left = 50
BPeditX2.Width = 45
BPeditRefreshTimerX2 = createTimer(getMainForm())
BPeditRefreshTimerX2.Interval = 500
BPeditRefreshTimerX2.onTimer = function(sender)
  if BPeditX2.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E0") then
  else
  setProperty(BPeditX2, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E0"))
 end
end
BPeditX3=createEdit(modelForm)
BPeditX3.Top = 120
BPeditX3.Left = 50
BPeditX3.Width = 45
BPeditRefreshTimerX3 = createTimer(getMainForm())
BPeditRefreshTimerX3.Interval = 500
BPeditRefreshTimerX3.onTimer = function(sender)
  if BPeditX3.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+EC") then
  else
  setProperty(BPeditX3, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+EC"))
 end
end
BPeditX4=createEdit(modelForm)
BPeditX4.Top = 190
BPeditX4.Left = 50
BPeditX4.Width = 45
BPeditRefreshTimerX4 = createTimer(getMainForm())
BPeditRefreshTimerX4.Interval = 500
BPeditRefreshTimerX4.onTimer = function(sender)
  if BPeditX4.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F8") then
  else
  setProperty(BPeditX4, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F8"))
 end
end
BPeditX5=createEdit(modelForm)
BPeditX5.Top = 260
BPeditX5.Left = 50
BPeditX5.Width = 45
BPeditRefreshTimerX5 = createTimer(getMainForm())
BPeditRefreshTimerX5.Interval = 500
BPeditRefreshTimerX5.onTimer = function(sender)
  if BPeditX5.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+104") then
  else
  setProperty(BPeditX5, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+104"))
 end
end
BPeditX6=createEdit(modelForm)
BPeditX6.Top = 330
BPeditX6.Left = 50
BPeditX6.Width = 45
BPeditRefreshTimerX6 = createTimer(getMainForm())
BPeditRefreshTimerX6.Interval = 500
BPeditRefreshTimerX6.onTimer = function(sender)
  if BPeditX6.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+11C") then
  else
  setProperty(BPeditX6, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+11C"))
 end
end
BPeditX7=createEdit(modelForm)
BPeditX7.Top = 400
BPeditX7.Left = 50
BPeditX7.Width = 45
BPeditRefreshTimerX7 = createTimer(getMainForm())
BPeditRefreshTimerX7.Interval = 500
BPeditRefreshTimerX7.onTimer = function(sender)
  if BPeditX7.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+110") then
  else
  setProperty(BPeditX7, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+110"))
 end
end
BPeditY2=createEdit(modelForm)
BPeditY2.Top = 50
BPeditY2.Left = 180
BPeditY2.Width = 45
BPeditRefreshTimerY2 = createTimer(getMainForm())
BPeditRefreshTimerY2.Interval = 500
BPeditRefreshTimerY2.onTimer = function(sender)
  if BPeditY2.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E8") then
  else
  setProperty(BPeditY2, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E8"))
 end
end
BPeditY3=createEdit(modelForm)
BPeditY3.Top = 120
BPeditY3.Left = 180
BPeditY3.Width = 45
BPeditRefreshTimerY3 = createTimer(getMainForm())
BPeditRefreshTimerY3.Interval = 500
BPeditRefreshTimerY3.onTimer = function(sender)
  if BPeditY3.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F4") then
  else
  setProperty(BPeditY3, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F4"))
 end
end
BPeditY4=createEdit(modelForm)
BPeditY4.Top = 190
BPeditY4.Left = 180
BPeditY4.Width = 45
BPeditRefreshTimerY4 = createTimer(getMainForm())
BPeditRefreshTimerY4.Interval = 500
BPeditRefreshTimerY4.onTimer = function(sender)
  if BPeditY4.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+100") then
  else
  setProperty(BPeditY4, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+100"))
 end
end
BPeditY5=createEdit(modelForm)
BPeditY5.Top = 260
BPeditY5.Left = 180
BPeditY5.Width = 45
BPeditRefreshTimerY5 = createTimer(getMainForm())
BPeditRefreshTimerY5.Interval = 500
BPeditRefreshTimerY5.onTimer = function(sender)
  if BPeditY5.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+10C") then
  else
  setProperty(BPeditY5, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+10C"))
 end
end
BPeditY6=createEdit(modelForm)
BPeditY6.Top = 330
BPeditY6.Left = 180
BPeditY6.Width = 45
BPeditRefreshTimerY6 = createTimer(getMainForm())
BPeditRefreshTimerY6.Interval = 500
BPeditRefreshTimerY6.onTimer = function(sender)
  if BPeditY6.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+124") then
  else
  setProperty(BPeditY6, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+124"))
 end
end
BPeditY7=createEdit(modelForm)
BPeditY7.Top = 400
BPeditY7.Left = 180
BPeditY7.Width = 45
BPeditRefreshTimerY7 = createTimer(getMainForm())
BPeditRefreshTimerY7.Interval = 500
BPeditRefreshTimerY7.onTimer = function(sender)
  if BPeditY7.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+118") then
  else
  setProperty(BPeditY7, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+118"))
 end
end
BPeditZ2=createEdit(modelForm)
BPeditZ2.Top = 50
BPeditZ2.Left = 310
BPeditZ2.Width = 45
BPeditRefreshTimerZ2 = createTimer(getMainForm())
BPeditRefreshTimerZ2.Interval = 500
BPeditRefreshTimerZ2.onTimer = function(sender)
  if BPeditZ2.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E4") then
  else
  setProperty(BPeditZ2, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+E4"))
 end
end
BPeditZ3=createEdit(modelForm)
BPeditZ3.Top = 120
BPeditZ3.Left = 310
BPeditZ3.Width = 45
BPeditRefreshTimerZ3 = createTimer(getMainForm())
BPeditRefreshTimerZ3.Interval = 500
BPeditRefreshTimerZ3.onTimer = function(sender)
  if BPeditZ3.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F0") then
  else
  setProperty(BPeditZ3, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+F0"))
 end
end
BPeditZ4=createEdit(modelForm)
BPeditZ4.Top = 190
BPeditZ4.Left = 310
BPeditZ4.Width = 45
BPeditZ4.Height = 15
BPeditRefreshTimerZ4 = createTimer(getMainForm())
BPeditRefreshTimerZ4.Interval = 500
BPeditRefreshTimerZ4.onTimer = function(sender)
  if BPeditZ4.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+FC") then
  else
  setProperty(BPeditZ4, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+FC"))
 end
end
BPeditZ5=createEdit(modelForm)
BPeditZ5.Top = 260
BPeditZ5.Left = 310
BPeditZ5.Width = 45
BPeditRefreshTimerZ5 = createTimer(getMainForm())
BPeditRefreshTimerZ5.Interval = 500
BPeditRefreshTimerZ5.onTimer = function(sender)
  if BPeditZ5.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+108") then
  else
  setProperty(BPeditZ5, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+108"))
 end
end
BPeditZ6=createEdit(modelForm)
BPeditZ6.Top = 330
BPeditZ6.Left = 310
BPeditZ6.Width = 45
BPeditRefreshTimerZ6 = createTimer(getMainForm())
BPeditRefreshTimerZ6.Interval = 500
BPeditRefreshTimerZ6.onTimer = function(sender)
  if BPeditZ6.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+120") then
  else
  setProperty(BPeditZ6, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+120"))
 end
end
BPeditZ7=createEdit(modelForm)
BPeditZ7.Top = 400
BPeditZ7.Left = 310
BPeditZ7.Width = 45
BPeditRefreshTimerZ7 = createTimer(getMainForm())
BPeditRefreshTimerZ7.Interval = 500
BPeditRefreshTimerZ7.onTimer = function(sender)
  if BPeditZ7.text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+114") then
  else
  setProperty(BPeditZ7, 'text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+114"))
 end
end
BPeditX2.Visible = false
BPeditX3.Visible = false
BPeditX4.Visible = false
BPeditX5.Visible = false
BPeditX6.Visible = false
BPeditX7.Visible = false
BPeditY2.Visible = false
BPeditY3.Visible = false
BPeditY4.Visible = false
BPeditY5.Visible = false
BPeditY6.Visible = false
BPeditY7.Visible = false
BPeditZ2.Visible = false
BPeditZ3.Visible = false
BPeditZ4.Visible = false
BPeditZ5.Visible = false
BPeditZ6.Visible = false
BPeditZ7.Visible = false
HBedit=createEdit(modelForm)
HBedit.Top = 175
HBedit.Left = 180
HBedit.Width = 35
HBeditRefreshTimer = createTimer(getMainForm())
HBeditRefreshTimer.Interval = 500
HBeditRefreshTimer.onTimer = function(sender)
  if HBedit.Text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8C") then
  else
  setProperty(HBedit, 'Text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+8C"))
 end
end
HBedit2=createEdit(modelForm)
HBedit2.Top = 275
HBedit2.Left = 180
HBedit2.Width = 35
HBeditRefreshTimer2 = createTimer(getMainForm())
HBeditRefreshTimer2.Interval = 500
HBeditRefreshTimer2.onTimer = function(sender)
  if HBedit2.Text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+88") then
  else
  setProperty(HBedit2, 'Text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+88"))
 end
end
HBedit3=createEdit(modelForm)
HBedit3.Top = 375
HBedit3.Left = 180
HBedit3.Width = 35
HBeditRefreshTimer3 = createTimer(getMainForm())
HBeditRefreshTimer3.Interval = 1500
HBeditRefreshTimer3.onTimer = function(sender)
  if HBedit3.Text == readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+84") then
  else
  setProperty(HBedit3, 'Text', readFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+84"))
 end
end
HBedit.Visible = false
HBedit2.Visible = false
HBedit3.Visible = false
--OnTopEdit
OnTopMainedit=createEdit(modelForm)
OnTopMainedit.Top = 50
OnTopMainedit.Left = 350
OnTopMainedit.Width = 40
OnTopMainedit2=createEdit(modelForm)
OnTopMainedit2.Top = 100
OnTopMainedit2.Left = 350
OnTopMainedit2.Width = 40
OnTopMainedit3=createEdit(modelForm)
OnTopMainedit3.Top = 150
OnTopMainedit3.Left = 350
OnTopMainedit3.Width = 40
OnTopMainedit4=createEdit(modelForm)
OnTopMainedit4.Top = 200
OnTopMainedit4.Left = 350
OnTopMainedit4.Width = 40
OnTopMainedit5=createEdit(modelForm)
OnTopMainedit5.Top = 250
OnTopMainedit5.Left = 350
OnTopMainedit5.Width = 40
OnTopMainedit6=createEdit(modelForm)
OnTopMainedit6.Top = 300
OnTopMainedit6.Left = 350
OnTopMainedit6.Width = 40
OnTopMainedit7=createEdit(modelForm)
OnTopMainedit7.Top = 350
OnTopMainedit7.Left = 350
OnTopMainedit7.Width = 40
OnTopMainedit8=createEdit(modelForm)
OnTopMainedit8.Top = 400
OnTopMainedit8.Left = 350
OnTopMainedit8.Width = 40
OnTopMainedit.Visible = false
OnTopMainedit2.Visible = false
OnTopMainedit3.Visible = false
OnTopMainedit4.Visible = false
OnTopMainedit5.Visible = false
OnTopMainedit6.Visible = false
OnTopMainedit7.Visible = false
OnTopMainedit8.Visible = false
OnTopBSedit=createEdit(modelForm)
OnTopBSedit.Top = 50
OnTopBSedit.Left = 350
OnTopBSedit.Width = 40
OnTopBSedit2=createEdit(modelForm)
OnTopBSedit2.Top = 100
OnTopBSedit2.Left = 350
OnTopBSedit2.Width = 40
OnTopBSedit3=createEdit(modelForm)
OnTopBSedit3.Top = 150
OnTopBSedit3.Left = 350
OnTopBSedit3.Width = 40
OnTopBSedit4=createEdit(modelForm)
OnTopBSedit4.Top = 200
OnTopBSedit4.Left = 350
OnTopBSedit4.Width = 40
OnTopBSedit5=createEdit(modelForm)
OnTopBSedit5.Top = 250
OnTopBSedit5.Left = 350
OnTopBSedit5.Width = 40
OnTopBSedit6=createEdit(modelForm)
OnTopBSedit6.Top = 300
OnTopBSedit6.Left = 350
OnTopBSedit6.Width = 40
OnTopBSedit7=createEdit(modelForm)
OnTopBSedit7.Top = 350
OnTopBSedit7.Left = 350
OnTopBSedit7.Width = 40
OnTopBSedit8=createEdit(modelForm)
OnTopBSedit8.Top = 400
OnTopBSedit8.Left = 350
OnTopBSedit8.Width = 40
OnTopBSedit.Visible = false
OnTopBSedit2.Visible = false
OnTopBSedit3.Visible = false
OnTopBSedit4.Visible = false
OnTopBSedit5.Visible = false
OnTopBSedit6.Visible = false
OnTopBSedit7.Visible = false
OnTopBSedit8.Visible = false
OnTopBRedit2=createEdit(modelForm)
OnTopBRedit2.Top = 100
OnTopBRedit2.Left = 350
OnTopBRedit2.Width = 40
OnTopBRedit3=createEdit(modelForm)
OnTopBRedit3.Top = 150
OnTopBRedit3.Left = 350
OnTopBRedit3.Width = 40
OnTopBRedit4=createEdit(modelForm)
OnTopBRedit4.Top = 200
OnTopBRedit4.Left = 350
OnTopBRedit4.Width = 40
OnTopBRedit5=createEdit(modelForm)
OnTopBRedit5.Top = 250
OnTopBRedit5.Left = 350
OnTopBRedit5.Width = 40
OnTopBRedit6=createEdit(modelForm)
OnTopBRedit6.Top = 300
OnTopBRedit6.Left = 350
OnTopBRedit6.Width = 40
OnTopBRedit7=createEdit(modelForm)
OnTopBRedit7.Top = 350
OnTopBRedit7.Left = 350
OnTopBRedit7.Width = 40
OnTopBRedit8=createEdit(modelForm)
OnTopBRedit8.Top = 400
OnTopBRedit8.Left = 350
OnTopBRedit8.Width = 40
OnTopBRedit2.Visible = false
OnTopBRedit3.Visible = false
OnTopBRedit4.Visible = false
OnTopBRedit5.Visible = false
OnTopBRedit6.Visible = false
OnTopBRedit7.Visible = false
OnTopBRedit8.Visible = false
OnTopBPeditX2=createEdit(modelForm)
OnTopBPeditX2.Top = 50
OnTopBPeditX2.Left = 50
OnTopBPeditX2.Width = 45
OnTopBPeditX3=createEdit(modelForm)
OnTopBPeditX3.Top = 120
OnTopBPeditX3.Left = 50
OnTopBPeditX3.Width = 45
OnTopBPeditX4=createEdit(modelForm)
OnTopBPeditX4.Top = 190
OnTopBPeditX4.Left = 50
OnTopBPeditX4.Width = 45
OnTopBPeditX5=createEdit(modelForm)
OnTopBPeditX5.Top = 260
OnTopBPeditX5.Left = 50
OnTopBPeditX5.Width = 45
OnTopBPeditX6=createEdit(modelForm)
OnTopBPeditX6.Top = 330
OnTopBPeditX6.Left = 50
OnTopBPeditX6.Width = 45
OnTopBPeditX7=createEdit(modelForm)
OnTopBPeditX7.Top = 400
OnTopBPeditX7.Left = 50
OnTopBPeditX7.Width = 45
OnTopBPeditY2=createEdit(modelForm)
OnTopBPeditY2.Top = 50
OnTopBPeditY2.Left = 180
OnTopBPeditY2.Width = 45
OnTopBPeditY3=createEdit(modelForm)
OnTopBPeditY3.Top = 120
OnTopBPeditY3.Left = 180
OnTopBPeditY3.Width = 45
OnTopBPeditY4=createEdit(modelForm)
OnTopBPeditY4.Top = 190
OnTopBPeditY4.Left = 180
OnTopBPeditY4.Width = 45
OnTopBPeditY5=createEdit(modelForm)
OnTopBPeditY5.Top = 260
OnTopBPeditY5.Left = 180
OnTopBPeditY5.Width = 45
OnTopBPeditY6=createEdit(modelForm)
OnTopBPeditY6.Top = 330
OnTopBPeditY6.Left = 180
OnTopBPeditY6.Width = 45
OnTopBPeditY7=createEdit(modelForm)
OnTopBPeditY7.Top = 400
OnTopBPeditY7.Left = 180
OnTopBPeditY7.Width = 45
OnTopBPeditZ2=createEdit(modelForm)
OnTopBPeditZ2.Top = 50
OnTopBPeditZ2.Left = 310
OnTopBPeditZ2.Width = 45
OnTopBPeditZ3=createEdit(modelForm)
OnTopBPeditZ3.Top = 120
OnTopBPeditZ3.Left = 310
OnTopBPeditZ3.Width = 45
OnTopBPeditZ4=createEdit(modelForm)
OnTopBPeditZ4.Top = 190
OnTopBPeditZ4.Left = 310
OnTopBPeditZ4.Width = 45
OnTopBPeditZ4.Height = 15
OnTopBPeditZ5=createEdit(modelForm)
OnTopBPeditZ5.Top = 260
OnTopBPeditZ5.Left = 310
OnTopBPeditZ5.Width = 45
OnTopBPeditZ6=createEdit(modelForm)
OnTopBPeditZ6.Top = 330
OnTopBPeditZ6.Left = 310
OnTopBPeditZ6.Width = 45
OnTopBPeditZ7=createEdit(modelForm)
OnTopBPeditZ7.Top = 400
OnTopBPeditZ7.Left = 310
OnTopBPeditZ7.Width = 45
OnTopBPeditX2.Visible = false
OnTopBPeditX3.Visible = false
OnTopBPeditX4.Visible = false
OnTopBPeditX5.Visible = false
OnTopBPeditX6.Visible = false
OnTopBPeditX7.Visible = false
OnTopBPeditY2.Visible = false
OnTopBPeditY3.Visible = false
OnTopBPeditY4.Visible = false
OnTopBPeditY5.Visible = false
OnTopBPeditY6.Visible = false
OnTopBPeditY7.Visible = false
OnTopBPeditZ2.Visible = false
OnTopBPeditZ3.Visible = false
OnTopBPeditZ4.Visible = false
OnTopBPeditZ5.Visible = false
OnTopBPeditZ6.Visible = false
OnTopBPeditZ7.Visible = false
OnTopHBedit=createEdit(modelForm)
OnTopHBedit.Top = 175
OnTopHBedit.Left = 180
OnTopHBedit.Width = 35
OnTopHBedit2=createEdit(modelForm)
OnTopHBedit2.Top = 275
OnTopHBedit2.Left = 180
OnTopHBedit2.Width = 35
OnTopHBedit3=createEdit(modelForm)
OnTopHBedit3.Top = 375
OnTopHBedit3.Left = 180
OnTopHBedit3.Width = 35
OnTopHBedit.Visible = false
OnTopHBedit2.Visible = false
OnTopHBedit3.Visible = false
SetOnTopEdit = createButton(modelForm)
SetOnTopEdit.Caption = 'Set'
SetOnTopEdit.Top = 435
SetOnTopEdit.Left = 350
SetOnTopEdit.Width = 40
setMethodProperty(OnTopMainedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopMainedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBSedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBRedit8, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditX7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditY7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ4, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ5, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ6, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopBPeditZ7, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopHBedit, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopHBedit2, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
setMethodProperty(OnTopHBedit3, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
--SendOnEditBox
SetOnTopEdit.OnClick = function (sender)
  setProperty(OnTopMainedit, 'text', slider.Position)
  setProperty(OnTopMainedit2, 'text', slider2.Position)
  setProperty(OnTopMainedit3, 'text', slider3.Position)
  setProperty(OnTopMainedit4, 'text', slider4.Position)
  setProperty(OnTopMainedit5, 'text', slider5.Position)
  setProperty(OnTopMainedit6, 'text', slider6.Position)
  setProperty(OnTopMainedit7, 'text', slider7.Position)
  setProperty(OnTopMainedit8, 'text', slider8.Position)
  setProperty(OnTopBSedit, 'text', sliderBS.Position*0.01)
  setProperty(OnTopBSedit2, 'text', sliderBS2.Position*0.01)
  setProperty(OnTopBSedit3, 'text', sliderBS3.Position*0.01)
  setProperty(OnTopBSedit4, 'text', sliderBS4.Position*0.01)
  setProperty(OnTopBSedit5, 'text', sliderBS5.Position*0.01)
  setProperty(OnTopBSedit6, 'text', sliderBS6.Position*0.01)
  setProperty(OnTopBSedit7, 'text', sliderBS7.Position*0.01)
  setProperty(OnTopBSedit8, 'text', sliderBS8.Position*0.01)
  setProperty(OnTopBRedit2, 'text', sliderBR2.Position)
  setProperty(OnTopBRedit3, 'text', sliderBR3.Position)
  setProperty(OnTopBRedit4, 'text', sliderBR4.Position)
  setProperty(OnTopBRedit5, 'text', sliderBR5.Position)
  setProperty(OnTopBRedit6, 'text', sliderBR6.Position)
  setProperty(OnTopBRedit7, 'text', sliderBR7.Position)
  setProperty(OnTopBRedit8, 'text', sliderBR8.Position)
  setProperty(OnTopBPeditX2, 'text', sliderBPX.Position)
  setProperty(OnTopBPeditX3, 'text', sliderBPX2.Position)
  setProperty(OnTopBPeditX4, 'text', sliderBPX3.Position)
  setProperty(OnTopBPeditX5, 'text', sliderBPX4.Position)
  setProperty(OnTopBPeditX6, 'text', sliderBPX5.Position)
  setProperty(OnTopBPeditX7, 'text', sliderBPX6.Position)
  setProperty(OnTopBPeditY2, 'text', sliderBPY1.Position)
  setProperty(OnTopBPeditY3, 'text', sliderBPY2.Position)
  setProperty(OnTopBPeditY4, 'text', sliderBPY3.Position)
  setProperty(OnTopBPeditY5, 'text', sliderBPY4.Position)
  setProperty(OnTopBPeditY6, 'text', sliderBPY5.Position)
  setProperty(OnTopBPeditY7, 'text', sliderBPY6.Position)
  setProperty(OnTopBPeditZ2, 'text', sliderBPZ1.Position)
  setProperty(OnTopBPeditZ3, 'text', sliderBPZ2.Position)
  setProperty(OnTopBPeditZ4, 'text', sliderBPZ3.Position)
  setProperty(OnTopBPeditZ5, 'text', sliderBPZ4.Position)
  setProperty(OnTopBPeditZ6, 'text', sliderBPZ5.Position)
  setProperty(OnTopBPeditZ7, 'text', sliderBPZ6.Position)
  setProperty(OnTopHBedit, 'text', sliderHB.Position*0.01)
  setProperty(OnTopHBedit2, 'text', sliderHB2.Position*0.01)
  setProperty(OnTopHBedit3, 'text', sliderHB3.Position*0.01)
 if(checkbox_getState(toggle) == 1) and OnTopMainedit.visible == true then
OnTopMainedit.Visible = false
OnTopMainedit2.Visible = false
OnTopMainedit3.Visible = false
OnTopMainedit4.Visible = false
OnTopMainedit5.Visible = false
OnTopMainedit6.Visible = false
OnTopMainedit7.Visible = false
OnTopMainedit8.Visible = false
setProperty(slider, 'Position', getProperty(OnTopMainedit, 'text'))
setProperty(slider2, 'Position', getProperty(OnTopMainedit2, 'text'))
setProperty(slider3, 'Position', getProperty(OnTopMainedit3, 'text'))
setProperty(slider4, 'Position', getProperty(OnTopMainedit4, 'text'))
setProperty(slider5, 'Position', getProperty(OnTopMainedit5, 'text'))
setProperty(slider6, 'Position', getProperty(OnTopMainedit6, 'text'))
setProperty(slider7, 'Position', getProperty(OnTopMainedit7, 'text'))
setProperty(slider8, 'Position', getProperty(OnTopMainedit8, 'text'))
 elseif(checkbox_getState(toggleBS) == 1) and OnTopBSedit.visible == true then
OnTopBSedit.Visible = false
OnTopBSedit2.Visible = false
OnTopBSedit3.Visible = false
OnTopBSedit4.Visible = false
OnTopBSedit5.Visible = false
OnTopBSedit6.Visible = false
OnTopBSedit7.Visible = false
OnTopBSedit8.Visible = false
setProperty(sliderBS, 'Position', (round(tonumber(getProperty(OnTopBSedit, 'text')/0.01))))
setProperty(sliderBS2, 'Position', (round(tonumber(getProperty(OnTopBSedit2, 'text')/0.01))))
setProperty(sliderBS3, 'Position', (round(tonumber(getProperty(OnTopBSedit3, 'text')/0.01))))
setProperty(sliderBS4, 'Position', (round(tonumber(getProperty(OnTopBSedit4, 'text')/0.01))))
setProperty(sliderBS5, 'Position', (round(tonumber(getProperty(OnTopBSedit5, 'text')/0.01))))
setProperty(sliderBS6, 'Position', (round(tonumber(getProperty(OnTopBSedit6, 'text')/0.01))))
setProperty(sliderBS7, 'Position', (round(tonumber(getProperty(OnTopBSedit7, 'text')/0.01))))
setProperty(sliderBS8, 'Position', (round(tonumber(getProperty(OnTopBSedit8, 'text')/0.01))))
 elseif(checkbox_getState(toggleBR) == 1) and OnTopBRedit2.visible == true then
OnTopBRedit2.Visible = false
OnTopBRedit3.Visible = false
OnTopBRedit4.Visible = false
OnTopBRedit5.Visible = false
OnTopBRedit6.Visible = false
OnTopBRedit7.Visible = false
OnTopBRedit8.Visible = false
setProperty(sliderBR2, 'Position', getProperty(OnTopBRedit2, 'text'))
setProperty(sliderBR3, 'Position', getProperty(OnTopBRedit3, 'text'))
setProperty(sliderBR4, 'Position', getProperty(OnTopBRedit4, 'text'))
setProperty(sliderBR5, 'Position', getProperty(OnTopBRedit5, 'text'))
setProperty(sliderBR6, 'Position', getProperty(OnTopBRedit6, 'text'))
setProperty(sliderBR7, 'Position', getProperty(OnTopBRedit7, 'text'))
setProperty(sliderBR8, 'Position', getProperty(OnTopBRedit8, 'text'))
 elseif(checkbox_getState(toggleBP) == 1) and OnTopBPeditX2.visible == true then
OnTopBPeditX2.Visible = false
OnTopBPeditX3.Visible = false
OnTopBPeditX4.Visible = false
OnTopBPeditX5.Visible = false
OnTopBPeditX6.Visible = false
OnTopBPeditX7.Visible = false
setProperty(sliderBPX, 'Position', getProperty(OnTopBPeditX2, 'text'))
setProperty(sliderBPX2, 'Position', getProperty(OnTopBPeditX3, 'text'))
setProperty(sliderBPX3, 'Position', getProperty(OnTopBPeditX4, 'text'))
setProperty(sliderBPX4, 'Position', getProperty(OnTopBPeditX5, 'text'))
setProperty(sliderBPX5, 'Position', getProperty(OnTopBPeditX6, 'text'))
setProperty(sliderBPX6, 'Position', getProperty(OnTopBPeditX7, 'text'))
OnTopBPeditY2.Visible = false
OnTopBPeditY3.Visible = false
OnTopBPeditY4.Visible = false
OnTopBPeditY5.Visible = false
OnTopBPeditY6.Visible = false
OnTopBPeditY7.Visible = false
setProperty(sliderBPY, 'Position', getProperty(OnTopBPeditY2, 'text'))
setProperty(sliderBPY2, 'Position', getProperty(OnTopBPeditY3, 'text'))
setProperty(sliderBPY3, 'Position', getProperty(OnTopBPeditY4, 'text'))
setProperty(sliderBPY4, 'Position', getProperty(OnTopBPeditY5, 'text'))
setProperty(sliderBPY5, 'Position', getProperty(OnTopBPeditY6, 'text'))
setProperty(sliderBPY6, 'Position', getProperty(OnTopBPeditY7, 'text'))
OnTopBPeditZ2.Visible = false
OnTopBPeditZ3.Visible = false
OnTopBPeditZ4.Visible = false
OnTopBPeditZ5.Visible = false
OnTopBPeditZ6.Visible = false
OnTopBPeditZ7.Visible = false
setProperty(sliderBPZ, 'Position', getProperty(OnTopBPeditZ2, 'text'))
setProperty(sliderBPZ2, 'Position', getProperty(OnTopBPeditZ3, 'text'))
setProperty(sliderBPZ3, 'Position', getProperty(OnTopBPeditZ4, 'text'))
setProperty(sliderBPZ4, 'Position', getProperty(OnTopBPeditZ5, 'text'))
setProperty(sliderBPZ5, 'Position', getProperty(OnTopBPeditZ6, 'text'))
setProperty(sliderBPZ6, 'Position', getProperty(OnTopBPeditZ7, 'text'))
 elseif(checkbox_getState(toggleHB) == 1) and OnTopHBedit.visible == true then
OnTopHBedit.Visible = false
OnTopHBedit2.Visible = false
OnTopHBedit3.Visible = false
setProperty(sliderHB, 'Position', (round(tonumber(getProperty(OnTopHBedit, 'text')/0.01))))
setProperty(sliderHB2, 'Position', (round(tonumber(getProperty(OnTopHBedit2, 'text')/0.01))))
setProperty(sliderHB3, 'Position', (round(tonumber(getProperty(OnTopHBedit3, 'text')/0.01))))
 elseif(checkbox_getState(toggle) == 1) and OnTopMainedit.visible == false then
OnTopMainedit.Visible = true
OnTopMainedit2.Visible = true
OnTopMainedit3.Visible = true
OnTopMainedit4.Visible = true
OnTopMainedit5.Visible = true
OnTopMainedit6.Visible = true
OnTopMainedit7.Visible = true
OnTopMainedit8.Visible = true
 elseif(checkbox_getState(toggleBS) == 1) and OnTopBSedit.visible == false then
OnTopBSedit.Visible = true
OnTopBSedit2.Visible = true
OnTopBSedit3.Visible = true
OnTopBSedit4.Visible = true
OnTopBSedit5.Visible = true
OnTopBSedit6.Visible = true
OnTopBSedit7.Visible = true
OnTopBSedit8.Visible = true
 elseif(checkbox_getState(toggleBR) == 1) and OnTopBRedit2.visible == false then
OnTopBRedit2.Visible = true
OnTopBRedit3.Visible = true
OnTopBRedit4.Visible = true
OnTopBRedit5.Visible = true
OnTopBRedit6.Visible = true
OnTopBRedit7.Visible = true
OnTopBRedit8.Visible = true
 elseif(checkbox_getState(toggleBP) == 1) and OnTopBPeditX2.visible == false then
OnTopBPeditX2.Visible = true
OnTopBPeditX3.Visible = true
OnTopBPeditX4.Visible = true
OnTopBPeditX5.Visible = true
OnTopBPeditX6.Visible = true
OnTopBPeditX7.Visible = true
OnTopBPeditY2.Visible = true
OnTopBPeditY3.Visible = true
OnTopBPeditY4.Visible = true
OnTopBPeditY5.Visible = true
OnTopBPeditY6.Visible = true
OnTopBPeditY7.Visible = true
OnTopBPeditZ2.Visible = true
OnTopBPeditZ3.Visible = true
OnTopBPeditZ4.Visible = true
OnTopBPeditZ5.Visible = true
OnTopBPeditZ6.Visible = true
OnTopBPeditZ7.Visible = true
 elseif(checkbox_getState(toggleHB) == 1) and OnTopHBedit.visible == false then
OnTopHBedit.Visible = true
OnTopHBedit2.Visible = true
OnTopHBedit3.Visible = true
end
end



--MiscellaneousForm
local MiscForm = createForm(false)
MiscForm.Caption='Miscellaneous'
MiscForm.Height = 350
MiscForm.Top = 380
MiscForm.Left = 325
MiscForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox8, 0)
   return caHide
end
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(MiscForm, [[MiscForm.png]])
MidnightButton=createButton(MiscForm)
MidnightButton.Left = 5
MidnightButton.Top = 5
MidnightButton.Width = 45
MidnightButton.Height = 25
MidnightButton.Caption = 'Night'
MidnightButton.OnClick = function (sender)
 writeFloat("[cubeworld.exe+00551A80]+6FC", 0)
end
DawnButton=createButton(MiscForm)
DawnButton.Left = 45
DawnButton.Top = 35
DawnButton.Width = 50
DawnButton.Height = 15
DawnButton.Caption = 'Dawn'
DawnButton.OnClick = function (sender)
 writeFloat("[cubeworld.exe+00551A80]+6FC", 14400000)
end
NoonButton=createButton(MiscForm)
NoonButton.Left = 135
NoonButton.Top = 35
NoonButton.Width = 50
NoonButton.Height = 15
NoonButton.Caption = 'Noon'
NoonButton.OnClick = function (sender)
 writeFloat("[cubeworld.exe+00551A80]+6FC", 43200000)
end
DuskButton=createButton(MiscForm)
DuskButton.Left = 225
DuskButton.Top = 35
DuskButton.Width = 50
DuskButton.Height = 15
DuskButton.Caption = 'Dusk'
DuskButton.OnClick = function (sender)
 writeFloat("[cubeworld.exe+00551A80]+6FC", 72000000)
end
PauseButton=createToggleBox(MiscForm)
PauseButton.Left = 270
PauseButton.Top = 5
PauseButton.Width = 45
PauseButton.Height = 25
PauseButton.Caption = 'Pause'
PauseButton.OnChange = function (sender)
  if(checkbox_getState(PauseButton) == 1) then
local PauseGetValue = readFloat("[cubeworld.exe+00551A80]+6FC")
                    PauseTimer = createTimer(getMainForm())
                    PauseTimer.Interval = 500
                    PauseTimer.onTimer = function(sender)
                    writeFloat("[cubeworld.exe+00551A80]+6FC", PauseGetValue)
                    end
  elseif (checkbox_getState(PauseButton) == 0) then
PauseTimer.destroy()
  end
end
TimeTB = createTrackBar(MiscForm)
TimeTB.left = 50
TimeTB.top = 5
TimeTB.width = 220
TimeTB.height = 30
TimeTB.frequency = 1
TimeTB.Max = 864
TimeTB.Min = 0
TimeTBclock = createTimer(getMainForm())
TimeTBclock.Interval = 500
TimeTBclock.onTimer = function(sender)
  if (TimeTB.position/0.00001) == readFloat("[cubeworld.exe+00551A80]+6FC") then
  elseif readFloat("[cubeworld.exe+00551A80]+6FC") ~= nil then
  setProperty(TimeTB, 'Position', (round(tonumber(readFloat("[cubeworld.exe+00551A80]+6FC")*0.00001))))
 end
end
ClassComboValue=createEdit(MiscForm)
ClassComboValue.Visible=false
ClassComboValueTimer = createTimer(getMainForm())
ClassComboValueTimer.Interval = 200
ClassComboValueTimer.onTimer = function(sender)
 if getProcessIDFromProcessName("cubeworld.exe") ~= nil and MiscForm.Visible == true and readBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14C') ~= nil then
  setProperty(ClassComboValue, 'text', readBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14C'))
  else
end
end
ClassCombo=createComboBox(MiscForm)
ClassCombo.Width = 100
ClassCombo.top = 65
ClassCombo.left = 25
ClassComboitem = ClassCombo.getItems
ClassCombo.style = 'csDropDownList'
ClassCombo.items.add("Warrior")
ClassCombo.items.add("Ranger")
ClassCombo.items.add("Mage")
ClassCombo.items.add("Rogue")
ClassCombo.OnChange = function (sender)
 writeBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14C', (ClassCombo.ItemIndex)+1)
end
ClassComboTimer = createTimer(getMainForm())
ClassComboTimer.Interval = 500
ClassComboTimer.onTimer = function(sender)
 if tonumber(ClassComboValue.text) ~= nil and getProcessIDFromProcessName("cubeworld.exe") ~= nil and MiscForm.Visible == true then
 setProperty(ClassCombo, 'ItemIndex', (tonumber(ClassComboValue.text)-1))
 else
end
end
LabelTimerSpe= createTimer(getMainForm())
LabelTimerSpe.Interval = 500
LabelTimerSpe.onTimer = function(sender)
 if ClassCombo.ItemIndex == 0 then
 BerserkerSpe.Visible = true
 GuadianSpe.Visible = true
 SniperSpe.Visible = false
 ScoutSpe.Visible = false
 FireSpe.Visible = false
 WaterSpe.Visible = false
 AssassinSpe.Visible = false
 NinjaSpe.Visible = false
 elseif ClassCombo.ItemIndex == 1 then
 BerserkerSpe.Visible = false
 GuadianSpe.Visible = false
 SniperSpe.Visible = true
 ScoutSpe.Visible = true
 FireSpe.Visible = false
 WaterSpe.Visible = false
 AssassinSpe.Visible = false
 NinjaSpe.Visible = false
 elseif ClassCombo.ItemIndex == 2 then
 BerserkerSpe.Visible = false
 GuadianSpe.Visible = false
 SniperSpe.Visible = false
 ScoutSpe.Visible = false
 FireSpe.Visible = true
 WaterSpe.Visible = true
 AssassinSpe.Visible = false
 NinjaSpe.Visible = false
 elseif ClassCombo.ItemIndex == 3 then
 BerserkerSpe.Visible = false
 GuadianSpe.Visible = false
 SniperSpe.Visible = false
 ScoutSpe.Visible = false
 FireSpe.Visible = false
 WaterSpe.Visible = false
 AssassinSpe.Visible = true
 NinjaSpe.Visible = true
 end
end
SpeTB = createTrackBar(MiscForm)
SpeTB.left = 185
SpeTB.top = 60
SpeTB.width = 100
SpeTB.height = 30
SpeTB.frequency = 1
SpeTB.Max = 1
SpeTB.Min = 0
SpeTB.OnChange=function(sender)
 if getProcessIDFromProcessName("cubeworld.exe") ~= nil and readBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14C') ~= nil and SpeTB.position == 0 then
  writeBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14D', 0)
 elseif getProcessIDFromProcessName("cubeworld.exe") ~= nil and SpeTB.Position == 1 then
  writeBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14D', 1)
 end
end
SpeTBTimer=createTimer(getMainForm())
SpeTBTimer.Interval = 2500
SpeTBTimer.onTimer = function(sender)
 if getProcessIDFromProcessName("cubeworld.exe") ~= nil and readBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14C') ~= nil and MiscForm.Visible == true then
 setProperty(SpeTB, 'Position', readBytes('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+14D'))
 end
end
BerserkerSpe = createLabel(MiscForm)
BerserkerSpe.Font.Size = 10
BerserkerSpe.Font.Color = 0xffffff
BerserkerSpe.Font.Style = ('fsUnderline, fsBold')
BerserkerSpe.Caption = 'Berserker'
BerserkerSpe.Top = 90
BerserkerSpe.Left = 170
BerserkerSpe.Visible = false
GuadianSpe = createLabel(MiscForm)
GuadianSpe.Font.Size = 10
GuadianSpe.Font.Color = 0xffffff
GuadianSpe.Font.Style = ('fsUnderline, fsBold')
GuadianSpe.Caption = 'Guardian'
GuadianSpe.Top = 90
GuadianSpe.Left = 240
GuadianSpe.Visible = false
SniperSpe = createLabel(MiscForm)
SniperSpe.Font.Size = 10
SniperSpe.Font.Color = 0xffffff
SniperSpe.Font.Style = ('fsUnderline, fsBold')
SniperSpe.Caption = 'Sniper'
SniperSpe.Top = 90
SniperSpe.Left = 180
SniperSpe.Visible = false
ScoutSpe = createLabel(MiscForm)
ScoutSpe.Font.Size = 10
ScoutSpe.Font.Color = 0xffffff
ScoutSpe.Font.Style = ('fsUnderline, fsBold')
ScoutSpe.Caption = 'Scout'
ScoutSpe.Top = 90
ScoutSpe.Left = 255
ScoutSpe.Visible = false
FireSpe = createLabel(MiscForm)
FireSpe.Font.Size = 10
FireSpe.Font.Color = 0xffffff
FireSpe.Font.Style = ('fsUnderline, fsBold')
FireSpe.Caption = 'Fire'
FireSpe.Top = 90
FireSpe.Left = 185
FireSpe.Visible = false
WaterSpe = createLabel(MiscForm)
WaterSpe.Font.Size = 10
WaterSpe.Font.Color = 0xffffff
WaterSpe.Font.Style = ('fsUnderline, fsBold')
WaterSpe.Caption = 'Water'
WaterSpe.Top = 90
WaterSpe.Left = 250
WaterSpe.Visible = false
AssassinSpe = createLabel(MiscForm)
AssassinSpe.Font.Size = 10
AssassinSpe.Font.Color = 0xffffff
AssassinSpe.Font.Style = ('fsUnderline, fsBold')
AssassinSpe.Caption = 'Assassin'
AssassinSpe.Top = 90
AssassinSpe.Left = 175
AssassinSpe.Visible = false
NinjaSpe = createLabel(MiscForm)
NinjaSpe.Font.Size = 10
NinjaSpe.Font.Color = 0xffffff
NinjaSpe.Font.Style = ('fsUnderline, fsBold')
NinjaSpe.Caption = 'Ninja'
NinjaSpe.Top = 90
NinjaSpe.Left = 255
NinjaSpe.Visible = false
GoldEdit=createEdit(MiscForm)
GoldEdit.Width = 75
GoldEdit.Top = 125
GoldEdit.Left = 115
GoldEditTimer=createTimer(getMainForm())
GoldEditTimer.Interval = 500
GoldEditTimer.onTimer = function(sender)
 if getProcessIDFromProcessName("cubeworld.exe") ~= nil and MiscForm.Visible == true then
 setProperty(GoldEdit, 'Text', readInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AAC'))
 end
end
GoldEditOnTop=createEdit(MiscForm)
GoldEditOnTop.Width = 75
GoldEditOnTop.Top = 125
GoldEditOnTop.Left = 115
GoldEditOnTop.Visible = false
GoldSetButton=createToggleBox(MiscForm)
GoldSetButton.Top = 124
GoldSetButton.Left = 190
GoldSetButton.Width = 25
GoldSetButton.Caption = 'Set'
GoldSetButton.OnChange = function (sender)
setMethodProperty(GoldEditOnTop, "OnKeyPress", function (sender, key) local keynr = string.byte(key); if (keynr~=8) and (keynr~=45)and (keynr~=110) and (keynr~=13) and ((keynr<48) or (keynr>57)) then key=nil; end if (keynr==13 and not(sender.Caption == nil or sender.Caption == '')) then key = nil; end return key; end)
 if checkbox_getState(GoldSetButton) == 1 then
 GoldEditOnTop.Visible = true
 elseif checkbox_getState(GoldSetButton) == 0 then
 GoldEditOnTop.Visible = false
 writeInteger('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+AAC', tonumber(GoldEditOnTop.Text))
 end
end
EntityMod=createComboBox(MiscForm)
EntityMod.Width = 150
EntityMod.top = 160
EntityMod.left = 85
EntityModitem = EntityMod.getItems
EntityMod.style = 'csDropDownList'
EntityMod.items.add("Hands Up")
EntityMod.items.add("Hair Glow")
EntityMod.items.add("Boss Glow With Hp Boost")
EntityMod.items.add("Boss Hp Boost")
EntityMod.items.add("Mini Boss Hp Boost")
EntityMod.items.add("Ghost")
EntityMod.items.add("Petrified")
EntityMod.items.add("Possessed")
EntityMod.items.add(" ")
EntityMod.OnChange = function(sender)
 if EntityMod.ItemIndex == 0 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 1 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 2 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 3 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 4 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 5 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 6 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 1)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 elseif EntityMod.ItemIndex == 7 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 1)
 elseif EntityMod.ItemIndex == 8 then
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+80', 0, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+81', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 2, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 1, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 4, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+82', 6, 0)
 setbit('[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+83', 2, 0)
 end
end
CrouchToggle=createToggleBox(MiscForm)
CrouchToggle.Top = 325
CrouchToggle.Left = 125
CrouchToggle.Caption = 'Crouch'
CrouchToggle.OnChange = function (sender)
 if checkbox_getState(CrouchToggle) == 1 then
 setbit('[[[[[[cubeworld.exe+00551A80]+8]+78]+40]+0]+10]+129', 2, 1)
 elseif checkbox_getState(CrouchToggle) == 0 then
 setbit('[[[[[[cubeworld.exe+00551A80]+8]+78]+40]+0]+10]+129', 2, 0)
 end
end
FlipCB=CreateCheckBox(MiscForm)
FlipCB.Top = 250
FlipCB.Left = 10
FlipCB.OnChange = function (sender)
 if checkbox_getState(FlipCB) == 1 then
 FlipCBTimer=createTimer(getMainForm())
 FlipCBTimer.Interval = 9800
 FlipCBTimer.onTimer = function(sender)
 writeFloat('[[[[[[cubeworld.exe+00551A80]+10]+8]+40]+0]+10]+12C', 10000)
 end
 elseif checkbox_getState(FlipCB) == 0 then
 FlipCBTimer.destroy()
 end
end
FlipLabel=createLabel(MiscForm)
FlipLabel.Top = 250
FlipLabel.Left = 25
FlipLabel.Caption = 'Flip'
FlipLabel.Font.Size = 10
FlipLabel.Font.Color = 0xffffff
FlipLabel.Font.Style = ('fsUnderline, fsBold')
StunCB=CreateCheckBox(MiscForm)
StunCB.Top = 270
StunCB.Left = 10
StunCB.OnChange = function (sender)
 if checkbox_getState(StunCB) == 1 then
 StunCBTimer=createTimer(getMainForm())
 StunCBTimer.Interval = 9800
 StunCBTimer.onTimer = function(sender)
 writeFloat('[[[[[[cubeworld.exe+00551A80]+10]+8]+40]+0]+10]+130', 10000)
 end
 elseif checkbox_getState(StunCB) == 0 then
 StunCBTimer.destroy()
 end
end
StunLabel=createLabel(MiscForm)
StunLabel.Top = 270
StunLabel.Left = 25
StunLabel.Caption = 'Stun'
StunLabel.Font.Size = 10
StunLabel.Font.Color = 0xffffff
StunLabel.Font.Style = ('fsUnderline, fsBold')
HumpCB=CreateCheckBox(MiscForm)
HumpCB.Top = 290
HumpCB.Left = 10
HumpCB.OnChange = function (sender)
 if checkbox_getState(HumpCB) == 1 then
 HumpCBTimer=createTimer(getMainForm())
 HumpCBTimer.Interval = 9800
 HumpCBTimer.onTimer = function(sender)
 writeFloat('[[[[[[cubeworld.exe+00551A80]+10]+8]+40]+0]+10]+134', 10000)
 end
 elseif checkbox_getState(HumpCB) == 0 then
 HumpCBTimer.destroy()
 end
end
HumpLabel=createLabel(MiscForm)
HumpLabel.Top = 290
HumpLabel.Left = 25
HumpLabel.Caption = 'Hump'
HumpLabel.Font.Size = 10
HumpLabel.Font.Color = 0xffffff
HumpLabel.Font.Style = ('fsUnderline, fsBold')
SlowCB=CreateCheckBox(MiscForm)
SlowCB.Top = 310
SlowCB.Left = 10
SlowCB.OnChange = function (sender)
 if checkbox_getState(SlowCB) == 1 then
 SlowCBTimer=createTimer(getMainForm())
 SlowCBTimer.Interval = 250
 SlowCBTimer.onTimer = function(sender)
 writeFloat('[[[[[[cubeworld.exe+00551A80]+10]+8]+40]+0]+10]+138', 5000)
 end
 elseif checkbox_getState(SlowCB) == 0 then
 SlowCBTimer.destroy()
 end
end
SlowLabel=createLabel(MiscForm)
SlowLabel.Top = 310
SlowLabel.Left = 25
SlowLabel.Caption = 'Slow'
SlowLabel.Font.Size = 10
SlowLabel.Font.Color = 0xffffff
SlowLabel.Font.Style = ('fsUnderline, fsBold')
FastCB=CreateCheckBox(MiscForm)
FastCB.Top = 330
FastCB.Left = 10
FastCB.OnChange = function (sender)
 if checkbox_getState(FastCB) == 1 then
 FastCBTimer=createTimer(getMainForm())
 FastCBTimer.Interval = 250
 FastCBTimer.onTimer = function(sender)
 writeFloat('[[[[[[cubeworld.exe+00551A80]+10]+8]+40]+0]+10]+13C', 5000)
 end
 elseif checkbox_getState(FastCB) == 0 then
 FastCBTimer.destroy()
 end
end
FastLabel=createLabel(MiscForm)
FastLabel.Top = 330
FastLabel.Left = 25
FastLabel.Caption = 'Fast'
FastLabel.Font.Size = 10
FastLabel.Font.Color = 0xffffff
FastLabel.Font.Style = ('fsUnderline, fsBold')
HpCB=CreateCheckBox(MiscForm)
HpCB.Top = 230
HpCB.Left = 300
HpCB.OnChange = function(sender)
  if(checkbox_getState(HpCB) == 1) then
autoAssemble([[
aobscanmodule(MobDmgAOB,cubeworld.exe,F3 0F 5C 47 20 F3 0F 11 81)
alloc(newmem,$1000,"cubeworld.exe"+A8ED0)

label(code)
label(return)

newmem:

code:
  //subss xmm0,[rdi+20]
  addss xmm0,[rdi+20]
  jmp return

MobDmgAOB:
  jmp newmem
return:
registersymbol(MobDmgAOB)
]])
  elseif (checkbox_getState(HpCB) == 0) then
  autoAssemble([[
  MobDmgAOB:
  db F3 0F 5C 47 20
  unregistersymbol(MobDmgAOB)
  dealloc(newmem)
  ]])
  end
end
HpLabel=createLabel(MiscForm)
HpLabel.Top = 230
HpLabel.Left = 275
HpLabel.Caption = 'HP'
HpLabel.Font.Size = 10
HpLabel.Font.Color = 0xffffff
HpLabel.Font.Style = ('fsUnderline, fsBold')
MpCB=CreateCheckBox(MiscForm)
MpCB.Top = 250
MpCB.Left = 300
MpCB.OnChange = function(sender)
  if(checkbox_getState(MpCB) == 1) then
MpCBPauseTimer = createTimer(getMainForm())
MpCBPauseTimer.Interval = 10
MpCBPauseTimer.onTimer = function(sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+188", 1)
end
  elseif (checkbox_getState(MpCB) == 0) then
MpCBPauseTimer.destroy()
  end
end
MpLabel=createLabel(MiscForm)
MpLabel.Top = 250
MpLabel.Left = 275
MpLabel.Caption = 'MP'
MpLabel.Font.Size = 10
MpLabel.Font.Color = 0xffffff
MpLabel.Font.Style = ('fsUnderline, fsBold')
BlockCB=CreateCheckBox(MiscForm)
BlockCB.Top = 270
BlockCB.Left = 300
BlockCB.OnChange = function(sender)
  if(checkbox_getState(BlockCB) == 1) then
BlockCBPauseTimer = createTimer(getMainForm())
BlockCBPauseTimer.Interval = 10
BlockCBPauseTimer.onTimer = function(sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+184", 1)
end
  elseif (checkbox_getState(BlockCB) == 0) then
BlockCBPauseTimer.destroy()
  end
end
BlockLabel=createLabel(MiscForm)
BlockLabel.Top = 270
BlockLabel.Left = 260
BlockLabel.Caption = 'Block'
BlockLabel.Font.Size = 10
BlockLabel.Font.Color = 0xffffff
BlockLabel.Font.Style = ('fsUnderline, fsBold')
StamCB=CreateCheckBox(MiscForm)
StamCB.Top = 290
StamCB.Left = 300
StamCB.OnChange = function(sender)
  if(checkbox_getState(StamCB) == 1) then
StamCBPauseTimer = createTimer(getMainForm())
StamCBPauseTimer.Interval = 10
StamCBPauseTimer.onTimer = function(sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+9A0", 1)
end
  elseif (checkbox_getState(StamCB) == 0) then
StamCBPauseTimer.destroy()
  end
end
StamLabel=createLabel(MiscForm)
StamLabel.Top = 290
StamLabel.Left = 265
StamLabel.Caption = 'Stam'
StamLabel.Font.Size = 10
StamLabel.Font.Color = 0xffffff
StamLabel.Font.Style = ('fsUnderline, fsBold')
ComboCB=CreateCheckBox(MiscForm)
ComboCB.Top = 310
ComboCB.Left = 300
ComboCB.OnChange = function(sender)
  if(checkbox_getState(ComboCB) == 1) then
ComboCBPauseGetValue = readInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+70")
ComboCBPauseTimer = createTimer(getMainForm())
ComboCBPauseTimer.Interval = 10
ComboCBPauseTimer.onTimer = function(sender)
writeInteger("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+70", ComboCBPauseGetValue)
end
  elseif (checkbox_getState(ComboCB) == 0) then
ComboCBPauseTimer.destroy()
  end
end
ComboLabel=createLabel(MiscForm)
ComboLabel.Top = 310
ComboLabel.Left = 250
ComboLabel.Caption = 'Combo'
ComboLabel.Font.Size = 10
ComboLabel.Font.Color = 0xffffff
ComboLabel.Font.Style = ('fsUnderline, fsBold')
StealthCB=CreateCheckBox(MiscForm)
StealthCB.Top = 330
StealthCB.Left = 300
StealthCB.OnChange = function(sender)
  if(checkbox_getState(StealthCB) == 1) then
StealthCBPauseTimer = createTimer(getMainForm())
StealthCBPauseTimer.Interval = 10
StealthCBPauseTimer.onTimer = function(sender)
writeFloat("[[[[[cubeworld.exe+00551A80]+8]+40]+0]+10]+18C", 1)
end
  elseif (checkbox_getState(StealthCB) == 0) then
StealthCBPauseTimer.destroy()
  end
end
StealthLabel=createLabel(MiscForm)
StealthLabel.Top = 330
StealthLabel.Left = 250
StealthLabel.Caption = 'Stealth'
StealthLabel.Font.Size = 10
StealthLabel.Font.Color = 0xffffff
StealthLabel.Font.Style = ('fsUnderline, fsBold')
SpeedHackTrackBar = createTrackBar(MiscForm)
SpeedHackTrackBar.left = 0
SpeedHackTrackBar.top = 220
SpeedHackTrackBar.width = 100
SpeedHackTrackBar.height = 30
SpeedHackTrackBar.frequency = 1
SpeedHackTrackBar.Max = 5
SpeedHackTrackBar.Min = 1
SpeedHackTrackBar.OnChange=function(sender)
 if SpeedHackTrackBar.Position == 1 then
speedhack_setSpeed(1)
 elseif SpeedHackTrackBar.Position == 2 then
speedhack_setSpeed(2)
 elseif SpeedHackTrackBar.Position == 3 then
speedhack_setSpeed(3)
 elseif SpeedHackTrackBar.Position == 4 then
speedhack_setSpeed(4)
 elseif SpeedHackTrackBar.Position == 5 then
speedhack_setSpeed(5)
 end
end
SpeedHackLabel=createLabel(MiscForm)
SpeedHackLabel.Top = 205
SpeedHackLabel.Left = 15
SpeedHackLabel.Caption = 'Speed Hack'
SpeedHackLabel.Font.Size = 10
SpeedHackLabel.Font.Color = 0xffffff
SpeedHackLabel.Font.Style = ('fsUnderline, fsBold')


--MiscellaneousToggleButton OnMainForm
function UDF1_CEToggleBox8Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox8) == 1) then
MiscForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox8) == 0) then
MiscForm.hide()
  end
end


--InventoryForm
local InvForm = createForm(false)
InvForm.Caption='Inventory'
InvForm.Height = 150
InvForm.Top = 380
InvForm.Left = 325
InvForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox7, 0)
   return caHide
end
--InventoryToggleButton OnMainForm
function UDF1_CEToggleBox7Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox7) == 1) then
InvForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox7) == 0) then
InvForm.hide()
  end
end



--MovementForm
local MovForm = createForm(false)
MovForm.Caption='Movement'
MovForm.Height = 150
MovForm.Top = 380
MovForm.Left = 325
MovForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox11, 0)
   return caHide
end
--MovementToggleButton OnMainForm
function UDF1_CEToggleBox11Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox11) == 1) then
MovForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox11) == 0) then
MovForm.hide()
  end
end


--StatsForm
local StatsForm = createForm(false)
StatsForm.Caption='Stats'
StatsForm.Height = 150
StatsForm.Top = 380
StatsForm.Left = 325
StatsForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox10, 0)
   return caHide
end
--StatsToggleButton OnMainForm
function UDF1_CEToggleBox10Change(sender)
  if(checkbox_getState(UDF1_CEToggleBox10) == 1) then
StatsForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox10) == 0) then
StatsForm.hide()
  end
end



--SettingsForm
local SetForm = createForm(false)
SetForm.Caption='Settings'
SetForm.Width = 350
SetForm.Height = 450
SetForm.Top = 380
SetForm.Left = 325
SetForm.OnClose = function(sender)
   checkbox_setState(UDF1_CEToggleBox9, 0)
   return caHide
end
function attachBackground(wc, tblFile)
 local p = createPicture()
 p.loadFromStream(findTableFile(tblFile).Stream)
 wc.OnPaint = function (sender)
 local c = sender.getCanvas()
 local bitmap =p.getBitmap()
 c.draw(0,0,bitmap)
 end
end
attachBackground(SetForm, [[SettingsForm.png]])
LangSelLabel=createLabel(SetForm)
LangSelLabel.setCaption('IG Language:')
LangSelLabel.Font.Color = 0xffffff
LangSelLabel.Font.Size = 12
LangSelLabel.Font.Style = ('fsUnderline, fsBold')
LangSelLabel.Top = 49
LangSelLabel.Left = 10
LangSel=createComboBox(SetForm)
LangSel.Top = 50
LangSel.Left = 125
LangSel.Width = 50
LangSel.OnChange = function (sender)
 os.rename(""..ActualPath..'\\dict_en.xml', ""..ActualPath..'\\dict_en-bak.xml')
  os.rename(""..ActualPath..'\\dict_en.xml', ""..ActualPath..'\\dict_de-bak.xml')
   os.rename(""..ActualPath..'\\dict_en.xml', ""..ActualPath..'\\dict_fr-bak.xml')
 os.rename(""..ActualPath..'\\dict_de.xml', ""..ActualPath..'\\dict_de-bak.xml')
 os.rename(""..ActualPath..'\\dict_fr.xml', ""..ActualPath..'\\dict_fr-bak.xml')
 if LangSel.ItemIndex == 0 then
 os.rename(""..ActualPath..'\\dict_en-bak.xml', ""..ActualPath..'\\dict_en.xml')
 elseif LangSel.ItemIndex == 1 then
  os.rename(""..ActualPath..'\\dict_de-bak.xml', ""..ActualPath..'\\dict_en.xml')
 elseif LangSel.ItemIndex == 2 then
  os.rename(""..ActualPath..'\\dict_fr-bak.xml', ""..ActualPath..'\\dict_en.xml')
 elseif LangSel.ItemIndex == 3 then
 else
 os.rename(""..ActualPath..'\\dict_en-bak.xml', ""..ActualPath..'\\dict_en.xml')
end
end
LangSel.style = 'csDropDownList'
LangSel.items.add("EN")
LangSel.items.add("DE")
LangSel.items.add("FR")
PathShowValue=createEdit(SetForm)
PathShowValue.Top = 9
PathShowValue.Left = 52
PathShowValue.Width = 290
PathShowValueTimer = createTimer(getMainForm())
PathShowValueTimer.Interval = 500
PathShowValueTimer.onTimer = function(sender)
  if PathShowValue.text == settings.Value['Path'] then
  else
  setProperty(PathShowValue, 'text', settings.Value['Path'])
 end
end
PathEdit=createEdit(SetForm)
PathEdit.Top = 9
PathEdit.Left = 52
PathEdit.Width = 290
PathEdit.Visible = False
SetButtonPathEdit=createToggleBox(SetForm)
SetButtonPathEdit.Top = 7
SetButtonPathEdit.Left = 7
SetButtonPathEdit.Caption = 'Set'
SetButtonPathEdit.Width = 40
SetButtonPathEdit.OnChange = function (sender)
  if(checkbox_getState(SetButtonPathEdit) == 1) then
PathEdit.Visible = true
  elseif (checkbox_getState(SetButtonPathEdit) == 0) then
PathEdit.Visible = false
settings.Value['Path']= PathEdit.Text
Path=settings.Value['Path']
end
end

function UDF1_CEToggleBox9Click(sender)
  if(checkbox_getState(UDF1_CEToggleBox12) == 1) then
SetForm.show()
  elseif (checkbox_getState(UDF1_CEToggleBox12) == 0) then
SetForm.hide()
  end
end

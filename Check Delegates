#include <ButtonConstants.au3>
#include <String.au3>
#include <Array.au3>
#include <MsgBoxConstants.au3>
#include <EditConstants.au3>
#include <GUIConstantsEx.au3>
#include <StaticConstants.au3>
#include <WindowsConstants.au3>


#Region ### HOT KEYS

HotKeySet("{ESC}", "terminate") ;[ESC] TO EXIT SCRIPT

#EndRegion ### HOT KEYS


#Region ### START Koda GUI section ### Form=
$guicheckdelegates = GUICreate("CHECK DELEGATES", 171, 65, -1351, 205)
$Labelemail = GUICtrlCreateLabel("Email:", 8, 16, 32, 17)
$inputemail = GUICtrlCreateInput("", 40, 8, 121, 21)
GUICtrlSetBkColor(-1, 0xA6CAF0)
$buttoncheck = GUICtrlCreateButton("Check", 8, 32, 75, 25)
$buttonclear = GUICtrlCreateButton("Clear", 88, 32, 75, 25)
GUISetState(@SW_SHOW)


$pos = WinGetPos($guicheckdelegates)
WinMove($guicheckdelegates, "", @DesktopWidth - $pos[2], @DesktopHeight - $pos[3] - 30) ;30 = START task/tray menu
#EndRegion ### END Koda GUI section ###




While 1 ;GUI WHILE
	$nMsg = GUIGetMsg()
	Switch $nMsg

		Case $GUI_EVENT_CLOSE
			Exit

		Case $buttoncheck
			buttoncheck()

		Case $buttonclear
			buttonclear()

	EndSwitch
WEnd ;GUI WHILE END

Func buttoncheck()

	$email = GUICtrlRead($inputemail)
	$StringLength = StringLen($email)

	If $StringLength <= 0 Then
		MsgBox(0 + 48, "Warning", "Email address required.", 10)
	EndIf

	If $StringLength > 0 Then
		getdelegates()
	EndIf

EndFunc   ;==>buttoncheck

Func getdelegates()

	GUICtrlSetState($inputemail, $GUI_DISABLE)
	GUICtrlSetState($buttoncheck, $GUI_DISABLE)
	GUICtrlSetState($buttonclear, $GUI_DISABLE)

	ClipPut("")


	$email = GUICtrlRead($inputemail)

	Run ("gam.bat", "C:\Support\bin", @SW_SHOWMAXIMIZED)

;~ 	Local $CMDPID = Run("cmd.exe", "", @SW_SHOWMAXIMIZED)

;~ 	While ProcessExists($CMDPID) = 0
;~ 		Sleep(100)
;~ 	WEnd

;~ 	Sleep(500)
;~ 	Send("GAM")
;~ 	Send("{ENTER}")

	While WinExists('\\VM-KEN-INF04: cmd /k "cd \gam"') = 0
		Sleep(100)
	WEnd

	Sleep(500)
	Send("GAM USER ")
	Send($email)
	Send(" SHOW DELEGATES")
	Send(" & EXIT")
	Send("{ENTER}")

	WinWaitActive('\\VM-KEN-INF04: cmd /k "cd \gam"')


	While WinExists('\\VM-KEN-INF04: cmd /k "cd \gam"') = 1
		Sleep(100)

	WEnd

;~ While PixelGetColor(633, 554) = "0x000000"
;~  Sleep (3000)
;~  Send ("color A0")
;~  Send ("{ENTER}")
;~  WEnd


	Send("!{SPACE}")
	Send("E")
	Send("S")
	Send("!{SPACE}")
	Send("E")
	Send("Y")

	WinClose('Administrator: C:\Windows\system32\cmd.exe')

	$clipemail = ClipGet()
	$sHeader = $email
	$arrayrange = "|0:05"

	GUICtrlSetState($inputemail, $GUI_ENABLE)
	GUICtrlSetState($buttoncheck, $GUI_ENABLE)
	GUICtrlSetState($buttonclear, $GUI_ENABLE)

	Global $aResult = StringRegExp($clipemail, 'Delegate ID: (\w+.\w+\W\w+.\w+.\w+)', 3)
	_ArrayDelete($aResult, 0)
	_ArrayDisplay($aResult, "Delegates For:", Default, +64, Default, $sHeader, $arrayrange)


	ClipPut("")



	If WinExists('Delegates For:') = 0 Then

		MsgBox(0 + 48, "Warning", "No Delegates found for " & $email & ".", 10)

	EndIf


EndFunc   ;==>getdelegates





Func buttonclear()

	GUICtrlSetData($inputemail, "")

EndFunc   ;==>buttonclear

Func terminate()

	Exit

EndFunc   ;==>terminate

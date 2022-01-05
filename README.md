' Name: Lorenzo's BoGoHo Calculator
' Purpose: Determine the sale price of a Buy One, Get One Half-Off sale
' Programmer: Justin Blair on 11-10-21

Option Explicit On
Option Strict On
Option Infer Off

Public Class Form1

    Private Sub btnCalc_Click(sender As Object, e As EventArgs) Handles btnCalc.Click

        Dim dblItem1 As Double
        Dim dblItem2 As Double
        Dim dblItemTotal As Double
        Dim dblAmountSaved As Double

        Double.TryParse(lblItem1.Text, dblItem1)
        Double.TryParse(lblItem2.Text, dblItem2)

        ' Calculate which item is discounted and total cost.
        If dblItem2 < dblItem1 Then
            dblItemTotal = (dblItem2 * 0.5) + dblItem1
        Else
            dblItemTotal = (dblItem1 * 0.5) + dblItem2
        End If

        ' Calculate amount saved
        If dblItem2 < dblItem1 Then
            dblAmountSaved = dblItem2 * 0.5
        Else
            dblAmountSaved = dblItem1 * 0.5
        End If

        ' Round prices to two decimal places
        dblItemTotal = Math.Round(dblItemTotal, 2)
        dblAmountSaved = Math.Round(dblAmountSaved, 2)

        ' Display amounts.
        lblItemTotal.Text = dblItemTotal.ToString("C2")
        lblAmountSaved.Text = dblAmountSaved.ToString("C2")


    End Sub

    Private Sub btnExit_Click(sender As Object, e As EventArgs) Handles btnExit.Click
        Me.Close()
    End Sub

    Private Sub ClearOutput(sender As Object, e As EventArgs) _
        Handles lblAmountSaved.Click, lblItemTotal.Click,
        lblItem1.TextChanged, lblItem2.TextChanged

        lblAmountSaved.Text = String.Empty
        lblItemTotal.Text = String.Empty

    End Sub

    Private Sub txtItem1_KeyPress(sender As Object, e As KeyPressEventArgs) Handles lblItem1.KeyPress
        ' Accept only numbers, decimal point, and the Backspace key.

        e.Handled = Not (Char.IsDigit(e.KeyChar) Or e.KeyChar = ControlChars.Back Or e.KeyChar = ".")

    End Sub

    Private Sub txtItem2_KeyPress(sender As Object, e As KeyPressEventArgs) Handles lblItem2.KeyPress
        ' Accept only numbers, decimal point, and the Backspace key.

        e.Handled = Not (Char.IsDigit(e.KeyChar) Or e.KeyChar = ControlChars.Back Or e.KeyChar = ".")

    End Sub


    Private Sub frmMain_FormClosing(sender As Object, e As FormClosingEventArgs) Handles Me.FormClosing
        ' Verify that the user wants to exit the application.

        Dim dlgButton As DialogResult
        dlgButton = MessageBox.Show("Do you want to exit?", "Lorenzo's Calculator",
                                      MessageBoxButtons.YesNo, MessageBoxIcon.Exclamation)
        ' If the No button is selected, do not close the form.
        If dlgButton = DialogResult.No Then
            e.Cancel = True
        End If
    End Sub

    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load

    End Sub
End Class

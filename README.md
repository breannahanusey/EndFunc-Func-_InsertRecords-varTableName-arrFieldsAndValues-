# EndFunc-Func-_InsertRecords-varTableName-arrFieldsAndValues-
EndFunc  Func _InsertRecords($varTableName,$arrFieldsAndValues)     If Not IsObj($objConnection) Then Return -1     If Not IsArray($arrFieldsAndValues) Then Return -2     For $y = 1 To UBound($arrFieldsAndValues)-1         $strInsert = "INSERT INTO " &amp; $varTableName &amp; " ("         $varFieldCount = UBound($arrFieldsAndValues,2)-1         For $x = 0 To $varFieldCount             $strInsert &amp;= $arrFieldsAndValues[0][$x]             If $x &lt; $varFieldCount Then $strInsert &amp;= ","         Next         $strInsert &amp;= ") VALUES ("         For $x = 0 To $varFieldCount             $strInsert &amp;= "'" &amp; $arrFieldsAndValues[$y][$x] &amp; "'"             If $x &lt; $varFieldCount Then $strInsert &amp;= ","         Next         $strInsert &amp;= ");"         $objConnection.Execute($strInsert)         If $errADODB.number Then             If Msgbox(4+16+256,"Insert Record Error","Statement failed:" &amp; @CRLF &amp; $strInsert &amp; @CRLF &amp; @CRLF &amp; "Would you like to continue?") &lt;> 6 Then Return -3         EndIf     Next     Return 1 EndFunc

Updates to add the Print Another button to the DWC Print Status page.

Note this is for DWC 1.14rc1 only.

Changes include.

Line 914 to 915 in reprap.htm are replaced with -

```html

<pre>
  <button class="btn btn-warning disabled" id="btn_pause" title="Pause current print (M25)"><span class="glyphicon glyphicon-pause"></span> <span>Pause Print</span></button><BR><BR>

  <button class="btn btn-success" id="btn_printanother" title="Print Another"><span class="glyphicon glyphicon-play"></span> <span>Print Another</span></button><BR><BR>
</pre>
```

in dwc.js at line 3790 insert the new function.

<pre>
  $("#btn_printanother").click(function() {
    // DAFIND 
    var tmpfile = '';

    if (isPaused) {
      // Do nothing
    } else if (isPrinting) {
      // do nothing 
    }
    else if (isPrinting == false){

      tmpFile = document.getElementById("span_progress_left").innerHTML.replace("Printed ", "").replace(", 100% Complete", "");

      //if (tmpfile == '') {return true;}

      showConfirmationDialog(T("Print Another?"), T("Print another copy of " +  tmpFile + "?"), function() {
                    // Perform software reset
                    sendGCode("M32 " + tmpFile);
                  });

    }

  });
</pre>

Updates to add the Print Another button to the DWC Print Status page. This is a bodged workaround which shows the button at all times.  It also may have issues with odd filename characters,  hwoever its been working ok for me for a few weeks now.  Keep and backup of the orginal .gz files and you can also re upload them to replace this change.

Note this is for DWC 1.14rc1 only.

Changes include.

Line 914 to 915 in reprap.htm are replaced with -

```html

 <button class="btn btn-warning disabled" id="btn_pause" title="Pause current print (M25)"><span class="glyphicon glyphicon-pause"></span> <span>Pause Print</span></button><BR><BR>
 <button class="btn btn-success" id="btn_printanother" title="Print Another"><span class="glyphicon glyphicon-play"></span> <span>Print Another</span></button><BR><BR>
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


I used 7zip to extract and re gzip the .gz files, both gz files can then be uploaded in DWC under Settings -> Upload files.

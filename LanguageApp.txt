function translateText() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var lastRow = sheet.getLastRow();
  var lastColumn = sheet.getLastColumn();
  
  var sourceLanguage = sheet.getRange("A3").getValue();
  var targetLanguagesRange = sheet.getRange("B3:3");
  var targetLanguages = targetLanguagesRange.getValues()[0];
 
  var range = sheet.getRange("A4:A");
  var values = range.getValues();
  // Logger.log(lastRow);
  
  for (var i = 0; i < lastRow -1; i++) {
    var textToTranslate = values[i][0];
   if (textToTranslate) { 
      for (var j = 0; j < lastColumn -1; j++) {
       var translatedText = LanguageApp.translate(textToTranslate, sourceLanguage, targetLanguages[j]);
        Utilities.sleep(500);
        sheet.getRange(i + 4, j + 2).setValue(translatedText); 
      }
    }
  }
}

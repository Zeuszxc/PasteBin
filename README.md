# PasteBin

```
 private void SaveButton_Click_1(object sender, EventArgs e)
 {
     OleDbConnection thisConnection = new OleDbConnection(connectionString);
     string Ole = "SELECT * FROM SubjectFile";
     OleDbDataAdapter thisAdapter = new OleDbDataAdapter(Ole, thisConnection);
     OleDbCommandBuilder thisBuilder = new OleDbCommandBuilder(thisAdapter);
     DataSet thisDataSet = new DataSet();
     thisAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;
     thisAdapter.Fill(thisDataSet, "SubjectFile");

     DataRow findRow = thisDataSet.Tables["SubjectFile"].Rows.Find(SubjCodeTextBox.Text);

     if (findRow==null)
     {
         DataRow thisRow = thisDataSet.Tables["SubjectFile"].NewRow();
         thisRow["SFSUBJCODE"] = SubjCodeTextBox.Text;
         thisRow["SFSUBJDESC"] = DescriptionTextBox.Text;
         thisRow["SFSUBJUNITS"] = UnitsTextBox.Text;
         thisRow["SFSUBJREOFRNG"] = OfferingComboBox.Text.Substring(0, 1);
         thisRow["SFSUBJCATEGORY"] = CategoryComboBox.Text;
         thisRow["SFSUBJSTATUS"] = "AC";
         thisRow["SFSUBJCOURSECODE"] = CourseCodeComboBox.Text;
         thisRow["SFSUBJCURRCODE"] = CurriculumCodeTextBox.Text;

         thisDataSet.Tables["SubjectFile"].Rows.Add(thisRow);
         thisAdapter.Update(thisDataSet, "SubjectFile");

         //SAVE DATA TO SUBJPREQFILE//

         thisConnection = new OleDbConnection(connectionString);
         Ole = "SELECT * FROM SUBJECTPREQFILE";
         thisAdapter = new OleDbDataAdapter(Ole, thisConnection);
         thisBuilder = new OleDbCommandBuilder(thisAdapter);
         thisDataSet = new DataSet();
         thisAdapter.Fill(thisDataSet, "SubjectPreqFile");

         thisRow = thisDataSet.Tables["SubjectPreqFile"].NewRow();

         if (RequisiteTextBox.Text != string.Empty)
         {
             thisRow["SUBJCODE"] = SubjCodeTextBox.Text;
             thisRow["SUBJPRECODE"] = RequisiteTextBox.Text;
             if (PreRequisiteRadioButton.Checked == true)
             {
                 thisRow["SUBJPRECATEGORY"] = "PR";
             }

             else if (CoRequisiteRadioButton.Checked == true)
             {
                 thisRow["SUBJPRECATEGORY"] = "CR";
             }

             thisDataSet.Tables["SubjectPreqFile"].Rows.Add(thisRow);
             thisAdapter.Update(thisDataSet, "SubjectPreqFile");
         }

         MessageBox.Show("RECORDED");
     }
     else {
         MessageBox.Show("Duplicate Entry!");
     }

     


     //OleDbConnection requisiteConnection = new OleDbConnection(connectionString);
     //string requisite = "SELECT * FROM SUBJECTPREQFILE";
     //OleDbDataAdapter requisiteAdapter = new OleDbDataAdapter(requisite, requisiteConnection);
     //OleDbCommandBuilder requisiteBuilder = new OleDbCommandBuilder(requisiteAdapter);

     //thisAdapter.Fill(thisDataSet, "SUBJECTPREQFILE");

     ////setup primary key
     //DataColumn[] keys = new DataColumn[2];

     //keys[0] = thisDataSet.Tables["SUBJECTPREQFILE"].Columns["SUBJCODE"];
     //keys[1] = thisDataSet.Tables["SUBJECTPREQFILE"].Columns["SUBJPRECODE"];

     //String[] valuesToSearch = new string[2];
     //valuesToSearch[0] = SubjCodeTextBox.Text;
     //valuesToSearch[1] = RequisiteTextBox.Text;

     //DataRow findRequisiteRow = thisDataSet.Tables["SUBJECTPREQFILE"].Rows.Find(valuesToSearch);
     //if (findRequisiteRow == null)
     //{

     //    DataRow thisRequisiteRow = thisDataSet.Tables["SUBJECTPREQFILE"].NewRow();

     //    thisRequisiteRow["SUBJCODE"] = SubjCodeTextBox.Text;
     //    thisRequisiteRow["SUBJPRECODE"] = RequisiteTextBox.Text;
     //    thisDataSet.Tables["SUBJECTPREQFILE"].Rows.Add(thisRequisiteRow);
     //    thisAdapter.Update(thisDataSet, "SUBJECTPREQFILE");
     //    MessageBox.Show("Entries Recorded");
     //}
     //else
     //{
     //    MessageBox.Show("Duplicate Entry!");
     //}



 }
```

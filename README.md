# QuizApp

A simple Android quiz application built with Kotlin that tests user knowledge with multiple-choice questions and checkboxes.

---

## Overview

This app presents a quiz where users select answers from a combination of radio buttons and checkboxes. Upon submission, the app calculates the total score and displays the result in a dialog with the current date.

---

## Features

- Multiple choice question using RadioGroup (e.g., selecting a year).
- Multiple answers using CheckBoxes.
- Dynamic scoring based on selected answers.
- Result dialog showing quiz score and current date.
- Reset functionality to clear selections.

---

## How It Works

- The user selects one radio button option and any combination of checkboxes.
- On submission:
  - If the radio button selected is "1969", the user earns 50 points.
  - Checking **Boeing** adds 25 points.
  - Checking **Airbus** adds 25 points.
  - Checking **Ford** adds 0 points.
- The total score is shown in an AlertDialog.
- The user can reset the quiz or exit via the dialog.

---

## Code Highlights

```kotlin
val boeing = findViewById<CheckBox>(R.id.boeing)
val ford = findViewById<CheckBox>(R.id.ford)
val airbus = findViewById<CheckBox>(R.id.airbus)

val rg = findViewById<RadioGroup>(R.id.rg)
val sub = findViewById<Button>(R.id.btnSub)
val cancel = findViewById<Button>(R.id.cancel)

sub.setOnClickListener {
    val selectedOption: Int = rg.checkedRadioButtonId
    val radioButton = findViewById<RadioButton>(selectedOption)
    var year: String = radioButton.text.toString()
    
    var totalMark = 0
    if (year == "1969") totalMark += 50
    if (boeing.isChecked) totalMark += 25
    if (airbus.isChecked) totalMark += 25
    if (ford.isChecked) totalMark += 0

    AlertDialog.Builder(this)
        .setTitle("Quiz Results as at ${LocalDate.now()}")
        .setMessage("Congratulations you scored $totalMark %")
        .setPositiveButton("Yes") { dialog, _ ->
            dialog.dismiss()
            finish()
        }
        .setNegativeButton("Cancel") { dialog, _ ->
            dialog.dismiss()
        }
        .show()
}

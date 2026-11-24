# Workshop 01 – Addition of Two Numbers

## DATE : 24.11.2026

## AIM:

To develop an Android application to get two numbers from the user and display the summation value in a text box using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio (Minimum Required Version: Android Studio Arctic Fox)

## ALGORITHM:

**Step 1:** Open Android Studio and click on File → New → New Project.

**Step 2:** Enter the Application Name as Workshop and click Next.

**Step 3:** Select the Minimum SDK and click Next.

**Step 4:** Select Empty Views Activity and click Finish.

**Step 5:** Design the user interface using UI components in the activity_main.xml file.

**Step 6:** Add two EditText fields to get input numbers from the user.

**Step 7:** Add a Button to perform the addition operation.

**Step 8:** Write the Java code in the MainActivity.java file to get the two input values and calculate their sum.

**Step 9:** Display the summation value in the Result text box when the ADD button is clicked.

**Step 10:** Save and run the application in the Android emulator.

## PROGRAM 
/* Program to print the text “Addition Operation ”.

Developed by: VAZHIGA BANU S

Registeration Number : 212225040484 */

## MainActivity.Java 

```
package com.example.workshop; // Keep your actual package name here

import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import com.google.android.material.button.MaterialButton;
import com.google.android.material.textfield.TextInputEditText;
import java.text.DecimalFormat;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Link UI components
        TextInputEditText etFirstNumber = findViewById(R.id.etFirstNumber);
        TextInputEditText etSecondNumber = findViewById(R.id.etSecondNumber);
        MaterialButton btnAdd = findViewById(R.id.btnAdd);
        MaterialButton btnClear = findViewById(R.id.btnClear);
        TextInputEditText etResult = findViewById(R.id.etResult);

        // Calculate Sum button logic
        btnAdd.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String num1Str = etFirstNumber.getText() != null ? etFirstNumber.getText().toString().trim() : "";
                String num2Str = etSecondNumber.getText() != null ? etSecondNumber.getText().toString().trim() : "";

                if (num1Str.isEmpty() || num2Str.isEmpty()) {
                    Toast.makeText(MainActivity.this, "Please enter both numbers", Toast.LENGTH_SHORT).show();
                    return;
                }

                try {
                    double num1 = Double.parseDouble(num1Str);
                    double num2 = Double.parseDouble(num2Str);
                    double sum = num1 + num2;

                    // Format cleanly with commas and up to 4 decimal places (e.g., 1,250.5)
                    DecimalFormat formatter = new DecimalFormat("#,###.####");
                    etResult.setText(formatter.format(sum));

                    // Dismiss keyboard so user sees the result clearly
                    hideKeyboard();
                } catch (NumberFormatException e) {
                    Toast.makeText(MainActivity.this, "Please enter valid numeric values", Toast.LENGTH_SHORT).show();
                }
            }
        });

        // Reset button logic
        btnClear.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                etFirstNumber.setText("");
                etSecondNumber.setText("");
                etResult.setText("0");
                etFirstNumber.requestFocus();
            }
        });
    }

    private void hideKeyboard() {
        View view = this.getCurrentFocus();
        if (view != null) {
            InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
            imm.hideSoftInputFromWindow(view.getWindowToken(), 0);
        }
    }
}
```
## Activity_Main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#F3F4F6"
    android:fillViewport="true">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:orientation="vertical"
        android:padding="24dp">

        <!-- Elevated Main Card -->
        <com.google.android.material.card.MaterialCardView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:cardBackgroundColor="#FFFFFF"
            app:cardCornerRadius="24dp"
            app:cardElevation="6dp"
            app:strokeWidth="0dp">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="vertical"
                android:padding="28dp">

                <!-- Header Badge -->
                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:background="#EEF2FF"
                    android:paddingHorizontal="12dp"
                    android:paddingVertical="4dp"
                    android:text="MATH UTILITY"
                    android:textColor="#9D1DBD"
                    android:textSize="11sp"
                    android:textStyle="bold" />

                <!-- Title & Subtitle -->
                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="12dp"
                    android:text="Sum Calculator"
                    android:textColor="#111827"
                    android:textSize="26sp"
                    android:textStyle="bold" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginTop="4dp"
                    android:layout_marginBottom="24dp"
                    android:text="Enter two values below to compute their total."
                    android:textColor="#6B7280"
                    android:textSize="14sp" />

                <!-- First Number Input (Floating Label + Clear Button) -->
                <com.google.android.material.textfield.TextInputLayout
                    style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginBottom="16dp"
                    android:hint="First Number"
                    app:boxCornerRadiusBottomEnd="14dp"
                    app:boxCornerRadiusBottomStart="14dp"
                    app:boxCornerRadiusTopEnd="14dp"
                    app:boxCornerRadiusTopStart="14dp"
                    app:boxStrokeColor="#9416A8"
                    app:endIconMode="clear_text"
                    app:hintTextColor="#9D17B6">

                    <com.google.android.material.textfield.TextInputEditText
                        android:id="@+id/etFirstNumber"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:inputType="numberDecimal|numberSigned"
                        android:textColor="#111827"
                        android:textSize="16sp" />
                </com.google.android.material.textfield.TextInputLayout>

                <!-- Plus Divider Indicator -->
                <TextView
                    android:layout_width="36dp"
                    android:layout_height="36dp"
                    android:layout_gravity="center"
                    android:layout_marginBottom="16dp"
                    android:background="#EEF2FF"
                    android:gravity="center"
                    android:text="+"
                    android:textColor="#821895"
                    android:textSize="20sp"
                    android:textStyle="bold" />

                <!-- Second Number Input -->
                <com.google.android.material.textfield.TextInputLayout
                    style="@style/Widget.MaterialComponents.TextInputLayout.OutlinedBox"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginBottom="24dp"
                    android:hint="Second Number"
                    app:boxCornerRadiusBottomEnd="14dp"
                    app:boxCornerRadiusBottomStart="14dp"
                    app:boxCornerRadiusTopEnd="14dp"
                    app:boxCornerRadiusTopStart="14dp"
                    app:boxStrokeColor="#8D15A2"
                    app:endIconMode="clear_text"
                    app:hintTextColor="#8F1CA4">

                    <com.google.android.material.textfield.TextInputEditText
                        android:id="@+id/etSecondNumber"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:inputType="numberDecimal|numberSigned"
                        android:textColor="#111827"
                        android:textSize="16sp" />
                </com.google.android.material.textfield.TextInputLayout>

                <!-- Action Buttons Row -->
                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginBottom="24dp"
                    android:orientation="horizontal">

                    <com.google.android.material.button.MaterialButton
                        android:id="@+id/btnClear"
                        style="@style/Widget.MaterialComponents.Button.OutlinedButton"
                        android:layout_width="0dp"
                        android:layout_height="56dp"
                        android:layout_marginEnd="10dp"
                        android:layout_weight="1"
                        android:text="Reset"
                        android:textAllCaps="false"
                        android:textColor="#4B5563"
                        android:textSize="15sp"
                        app:cornerRadius="14dp"
                        app:strokeColor="#D1D5DB" />

                    <com.google.android.material.button.MaterialButton
                        android:id="@+id/btnAdd"
                        android:layout_width="0dp"
                        android:layout_height="56dp"
                        android:layout_weight="2"
                        android:backgroundTint="#9215A8"
                        android:text="Calculate Sum"
                        android:textAllCaps="false"
                        android:textColor="#FFFFFF"
                        android:textSize="15sp"
                        android:textStyle="bold"
                        app:cornerRadius="14dp" />
                </LinearLayout>

                <!-- Result Display Box (Read-Only Text Box) -->
                <com.google.android.material.textfield.TextInputLayout
                    style="@style/Widget.MaterialComponents.TextInputLayout.FilledBox"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:hint="Summation Result"
                    app:boxBackgroundColor="#EEF2FF"
                    app:boxCornerRadiusBottomEnd="14dp"
                    app:boxCornerRadiusBottomStart="14dp"
                    app:boxCornerRadiusTopEnd="14dp"
                    app:boxCornerRadiusTopStart="14dp"
                    app:boxStrokeWidth="0dp"
                    app:boxStrokeWidthFocused="0dp"
                    app:hintTextColor="#931BA8">

                    <com.google.android.material.textfield.TextInputEditText
                        android:id="@+id/etResult"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:clickable="false"
                        android:cursorVisible="false"
                        android:focusable="false"
                        android:gravity="end"
                        android:text="0"
                        android:textColor="#841597"
                        android:textSize="26sp"
                        android:textStyle="bold" />
                </com.google.android.material.textfield.TextInputLayout>

            </LinearLayout>
        </com.google.android.material.card.MaterialCardView>
    </LinearLayout>
</ScrollView>

```

## OUTPUT:

## MAINACTIVITY.JAVA:

<img width="1917" height="1142" alt="Screenshot 2026-11-24 091642" src="https://github.com/user-attachments/assets/42e4e980-4824-4b6d-a50e-d88d7f689ff4" />


## ACTIVITY_MAIN.XML:

<img width="1917" height="1137" alt="Screenshot 2026-11-24 091854" src="https://github.com/user-attachments/assets/e62012f4-7ad1-465a-9c11-ec35a4baefb2" />


## Addition operation:

<img width="1917" height="1133" alt="Screenshot 2026-11-24 091735" src="https://github.com/user-attachments/assets/e81c8738-2577-4764-8cf8-3c85ec02a192" />


## RESULT:

Thus, the Android application for the addition of two numbers was successfully developed and executed using Android Studio.

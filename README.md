# Calculator-App
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;

//BUS442
//TJ Larson

namespace _442_Project2
{

    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
        }

        //declare global variables x and y
        int x, y;

        private void yCheckBox_CheckedChanged(object sender, EventArgs e)
        {
            //disable yTextBox until check box is checked
            if (yCheckBox.Checked == false)
                yTextBox.Enabled = false;
            if (yCheckBox.Checked)
                yTextBox.Enabled = true;
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            //Open a dialog message box when exit is performed, if yes close form
            DialogResult dialog = MessageBox.Show("Are you sure you want to exit?", "Exit Confirmation",
                MessageBoxButtons.YesNo, MessageBoxIcon.Warning);
            if (dialog == DialogResult.Yes)
                this.Close();
        }

        private void clearButton_Click(object sender, EventArgs e)
        {
            //clear listbox
            resultsListBox.Items.Clear();
        }

        private void raisedButton_MouseHover(object sender, EventArgs e)
        {
            raisedButton.BackColor = Color.AliceBlue;
        }

        private void displayButton_Click(object sender, EventArgs e)
        {
            string currentLine;

            //read in text file by creating StreamReader object
            StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");

            resultsListBox.Items.Clear();
            while (recordsFile.EndOfStream == false)
            {
                currentLine = recordsFile.ReadLine();
                resultsListBox.Items.Add(currentLine);
            }
            recordsFile.Close();

            
        }

        private void xTextBox_KeyPress(object sender, KeyPressEventArgs e)
        {
            //Only allow digit, control characters, negative symbol and backspace
            if (!char.IsControl(e.KeyChar)          //If key is NOT (!) a control char
                && !char.IsDigit(e.KeyChar)
                && e.KeyChar != '-')                //and also NOT a digit

            {
                e.Handled = true;

                return;
            }
        }

        private void yTextBox_KeyPress(object sender, KeyPressEventArgs e)
        {
            //Only allow digit, control characters, negative symbol and backspace
            if (!char.IsControl(e.KeyChar)          //If key is NOT (!) a control char
                && !char.IsDigit(e.KeyChar)
                && e.KeyChar != '-')                //and also NOT a digit

            {
                e.Handled = true;

                return;
            }
        }

        private void xTextBox_Click(object sender, EventArgs e)
        {
            xTextBox.SelectAll();
        }

        private void yTextBox_TextChanged(object sender, EventArgs e)
        {

        }

        private void oneButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 1;
            else yTextBox.Text += 1;
        }

        private void twoButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 2;
            else yTextBox.Text += 2;
        }

        private void threeButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 3;
            else yTextBox.Text += 3;
        }

        private void fourButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 4;
            else yTextBox.Text += 4;
        }

        private void fiveButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 5;
            else yTextBox.Text += 5;
        }

        private void sixButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 6;
            else yTextBox.Text += 6;
        }

        private void sevenButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 7;
            else yTextBox.Text += 7;
        }

        private void eightButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 8;
            else yTextBox.Text += 8;
        }

        private void nineButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 9;
            else yTextBox.Text += 9;
        }

        private void zeroButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text += 0;
            else yTextBox.Text += 0;
        }

        private void cancelButton_Click(object sender, EventArgs e)
        {
            if (yCheckBox.Checked == false)
                xTextBox.Text = null;
            else yTextBox.Text = null;
        }

        private void cancelEntryButton_Click(object sender, EventArgs e)
        {
            //parse text boxes
            xTextBox.Text = x.ToString();
            yTextBox.Text = y.ToString();


            string entryMinusOne = x.ToString();

            if (yCheckBox.Checked == false)
            {
                if (xTextBox.Text.Length > 0)
                {
                    entryMinusOne = xTextBox.Text;
                    entryMinusOne = entryMinusOne.Substring(0, entryMinusOne.Length - 1);
                }
                xTextBox.Text = entryMinusOne;
            }
            else if (yCheckBox.Checked == true)
            {
                if (yTextBox.Text.Length > 0)
                {
                    entryMinusOne = yTextBox.Text;
                    entryMinusOne = entryMinusOne.Substring(0, entryMinusOne.Length - 1);
                }
                yTextBox.Text = entryMinusOne;
            }
            else
            {

            }
            
        }

        private void raisedButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes and store in x and y 
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

           

            //declare new variable
            double raised;

            //perform function
            raised = Math.Pow(x, y);

            //clear list box
            resultsListBox.Items.Clear();
            //display in list box
            resultsListBox.Items.Add(x + " raised to the power of " + y + ": " + raised);

            
            
        }

        private void dividedButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes and store in x and y 
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            //declare new variable to store result of x/y
            double divided;

            //specify parameter
            if (y == 0)
            {
                //clear list box
                resultsListBox.Items.Clear();
                //display error
                resultsListBox.Items.Add("Can't divide by 0");
            }
            
            else
            {
                //perform function
                divided = (double)x / (double)y;

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add("Quotient of " + x +  " divided by " + y + ": " + divided);
            }

            
        }

        private void addButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes and store in x and y variables
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            //declare new variable to store result of x + y
            int added;

            //perform function
            added = x + y;

            //clear list box
            resultsListBox.Items.Clear();
            //Display in list box
            resultsListBox.Items.Add("Sum of " + x + " and " + y + ": " + added);

        }

        private void subtractButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes and store in x and y variables
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            //declare new variable to store result of x + y
            int subtracted;

            //perform function
            subtracted = x - y;

            //clear list box
            resultsListBox.Items.Clear();
            //Display in list box
            resultsListBox.Items.Add("Difference of " + x + " and " + y + ": " + subtracted);
        }

        private void reciprocalButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text box and store to x
            int.TryParse(xTextBox.Text, out x); 

            //declare reciprocal variable
            double recip;

            //provide error message if x = 0
            if (x == 0)
            {
                //clear list box
                resultsListBox.Items.Clear();
                //display error
                resultsListBox.Items.Add("Can't divide by 0");
            }

            else
            {
                //cast int x to double type
                double num = x;

                recip = 1 / num;

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add("Reciprocal of " + num + ": " + recip);
            }
            
        }

        private void factorialButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text box and store to x
            int.TryParse(xTextBox.Text, out x);

            //declare factorial variable
            int fact = x;
            int number = x - 1;

            //specify parameters
            if (x < -1 || x > 10)
            {
                resultsListBox.Items.Add("X must be between 0 and 10");
            }
            //test for case of x = 1;
            else if (x == 1 )
            {

                fact = fact * number;

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add(x + "!" + ":" + fact);
            }
            //test for case of x = 0
            else if (x == 0)
            {
                fact = fact ^ 1;

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add(x + "!" + ":" + fact);
            }
           
            else
            {
                //loop to perform factorial function
                while (number > 0) 
                {
                    //accumulate factorial variable
                    fact = fact * number;
                    number--;
                    
                }

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add(x + "!" + ":" + fact);

            }
        }

        private void xTextBox_TextChanged(object sender, EventArgs e)
        {
            xTextBox.SelectAll();
        }

        
        private void arrayValueButton_Click(object sender, EventArgs e)
        {
            //parse text boxes
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            //set parameters for entry
            if (x > 5 && y > 4)
            {
                //clear list box
                resultsListBox.Items.Clear();
                resultsListBox.Items.Add("X can't be greater than 6");
                resultsListBox.Items.Add("Y can't be greater than 5");
            }
            else
            {
                //declare 2D array (6 rows, 5 columns)
                string currentLine;
                string[,] records = new string[6, 5];
                string[] fields = new string[2];
                int row = 0, column = 0;

                //create streamreader
                StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");
                //read each line of the file
                while (recordsFile.EndOfStream == false)
                {
                    currentLine = recordsFile.ReadLine();
                    //split by comma
                    fields = currentLine.Split(',');         
                    //store in 2d array
                    for (column = 0; column <= 4; column++)
                        records[row, column] = fields[column];
                    row = row + 1;

                }

                //clear list box
                resultsListBox.Items.Clear();
                //display in list box
                resultsListBox.Items.Add("Value is: " + records[x, y]);

                recordsFile.Close();
            }

            
        }

        private void maxButton_Click(object sender, EventArgs e)
        {
            //create 1d array named records
            string[] records = new string[30];
            string currentLine;
            double max = 1032;

            //create StreamReader object to read numbers file
            StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");

            //clear listbox
            resultsListBox.Items.Clear();

            while (recordsFile.EndOfStream == false)
            {
                currentLine = recordsFile.ReadLine();

                //split the string data and store in records array
                records = currentLine.Split(',');

                //loop
                for (int a = 0; a <= 4; a++)
                {
                    if (double.Parse(records[a]) > max)
                    {
                        max = double.Parse(records[a]);
                    }


                    else
                    {

                    }

                }
            }
            //display the max file value (record[0])
            resultsListBox.Items.Add("Max file number is: " + max);
        }

        private void primeButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //Declare variables
            double prime;

            // Parse user inputs
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            if (x > y || x <= 0 || y <= 0 || x > 500 || y > 500)
            {
                //clear list box
                resultsListBox.Items.Clear();
                //display error
                resultsListBox.Items.Add("X must be less than Y");
                resultsListBox.Items.Add("X and Y must be greater than 0 and less than 500");
            }

            else
            {
                for (prime = x; prime <= y; prime++)
                {
                    bool primeNumber = true;
                    for (double a = 2; a < prime; a++)
                    {
                        if ((prime % a) == 0)
                        {
                            primeNumber = false;
                        }
                        else if (primeNumber == false)
                        {
                            break;
                        }
                        
                    }
                    if (primeNumber == true)
                    {
                        resultsListBox.Items.Add(prime + " is a prime number");
                    }
                    else
                    {
                        resultsListBox.Items.Add(prime + " is not a prime number");
                    }
                }
            }
        }

        private void squaresButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes to x and y 
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            //declare new variables
            double xSquare = 0, ySquare = 0, inputSum = 0, squareSum = 0;

            //if loop 
            if (x == 0 || y == 0)
            {
                //clear list box
                resultsListBox.Items.Add("X and Y can't be zero");
            }
            else if (x > y)
            {
                //display error message
                resultsListBox.Items.Clear();
                resultsListBox.Items.Add("X must be less than Y");
            }
            else if (x > 0 && y > 0)
            {
                //calculate new variables
                xSquare = x * x;
                ySquare = y * y;
                inputSum = x + y;
                squareSum = xSquare + ySquare;

                //clear list box
                resultsListBox.Items.Clear();
                //display in listbox
                resultsListBox.Items.Add("The number is: " + x + " and its square is: " + xSquare);
                resultsListBox.Items.Add("The number is: " + y + " and its square is: " + ySquare);
                resultsListBox.Items.Add("");
                resultsListBox.Items.Add("Sum of numbers: " + inputSum + " Sum of squares: " + squareSum);
            }

            

            else
            {

            }

        }

        private void sumButton_Click(object sender, EventArgs e)
        {
            //declare new variables
            string currentLine;
            string[] records;
            double sum =0;
            
            //read text file in
            StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");

            while (recordsFile.EndOfStream == false)
            {
                currentLine = recordsFile.ReadLine();
                //split the string data and store in records array
                records = currentLine.Split(',');

                //use sum to accumulate records
                  sum += (double.Parse(records[0]) + double.Parse(records[1]) + double.Parse(records[2]) + double.Parse(records[3]) +
                    double.Parse(records[4]));
            }

            //clear list box
            resultsListBox.Items.Clear();
            //display in list box
            resultsListBox.Items.Add("Sum of file numbers is: " + sum);
        }

        private void stdevButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes
            int.TryParse(xTextBox.Text, out x);
            int.TryParse(yTextBox.Text, out y);

            double tempX = 0, tempY = 0;
            //clear list box
            resultsListBox.Items.Clear();

            //declare new variables
            double a, mean, stdDev = 0, total = 0;

            //if x is greater than y flip the variables
            if (x > y)
            {
                tempX = Convert.ToDouble(y);
                tempY = Convert.ToDouble(x);

                //declare new variables


                //calculate mean
                mean = (tempX + tempY) / 2;


                //for loop to calculate 
                for (a = tempX; a <= tempY; a++)
                {
                    stdDev += Math.Pow(a - mean, 2);
                }

                //take square root to find total standard deviation
                total = Math.Sqrt(stdDev / (tempY - tempX));

                //display in list box
                resultsListBox.Items.Add("Standard deviation for range " + x + " to "
                    + y + ": " + total.ToString("N4"));

            }
            else
            {
                //calculate mean
                mean = (x + y) / 2;


                //for loop to calculate 
                for (a = x; a <= y; a++)
                {
                    stdDev += Math.Pow(a - mean, 2);
                }

                //take square root to find total standard deviation
                total = Math.Sqrt(stdDev / (y - x));

                //display in list box
                resultsListBox.Items.Add("Standard deviation for range " + x + " to "
                    + y + ": " + total.ToString("N4"));
            }

        }

        private void multTableButton_Click(object sender, EventArgs e)
        {
            if (xTextBox.Text.Trim() == string.Empty && yTextBox.Text.Trim() == string.Empty)
            {
                resultsListBox.Items.Add("Please enter X or Y, or both");
                return; // return because we don't want to run normal code of buton click
            }

            //parse text boxes
            int.TryParse(xTextBox.Text, out x);

            //declare new variable
            int mult = 0;

            //clear list box
            resultsListBox.Items.Clear();

            //limit user input to between 1 and 12
            if (x <= 0 || x > 12)
            {
                resultsListBox.Items.Add("X must be between 1 and 12");
            }
            else
            {
                //loop that calculates multiplication table
                for (int a = 1; a <= 12; a++)
                {

                    mult = a * x;

                    //display in list box
                    resultsListBox.Items.Add(a + " * " + x + " = " + mult);
                }
            }
        }

        private void avgButton_Click(object sender, EventArgs e)
        {
            //declare new variables
            string[] records = new string[30];
            string currentLine;
            double count, recordCount, sum = 0, avg = 0;



            count = records.Length;

            //read text file in
            StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");

            while (recordsFile.EndOfStream == false)
            {
                currentLine = recordsFile.ReadLine();
                //split the string data and store in records array
                records = currentLine.Split(',');
                
                //use sum to accumulate records
                sum += (double.Parse(records[0]) + double.Parse(records[1]) + double.Parse(records[2]) +
                    double.Parse(records[3]) + double.Parse(records[4]));

                
                
            }
            recordCount = count;
            
            //take average
            avg = sum / count;

            //clear list box
            resultsListBox.Items.Clear();
            //display in list box
            resultsListBox.Items.Add("Avg of file numbers is: " + avg.ToString("N5"));
            

            
        }
            private void rangeButton_Click(object sender, EventArgs e)
        {
            //declare new variables
            string currentLine;
            string[] records;
            double high = 1032, low = 8;

            //read text file in
            StreamReader recordsFile = new StreamReader(@"C:\Users\TJ Larson\Desktop\numbers.txt");

            while (recordsFile.EndOfStream == false)
            {
                currentLine = recordsFile.ReadLine();
                //split the string data and store in records array
                records = currentLine.Split(',');

                for (int a = 0; a <= 4; a++)
                {
                    if (double.Parse(records[a]) > high)
                    {
                        high = double.Parse(records[a]);
                    }

                    else if (double.Parse(records[a]) < low)
                    {
                        low = double.Parse(records[a]);
                    }

                    else
                    {

                    }
                }


            }

            double range = high - low;

            //clear list box
            resultsListBox.Items.Clear();
            //display in list box
            resultsListBox.Items.Add("Range of file values: " + range);
        }

        private void yTextBox_Click(object sender, EventArgs e)
        {
            yTextBox.SelectAll();
        }
    }
}

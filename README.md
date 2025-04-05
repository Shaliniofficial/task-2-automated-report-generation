# task-2-automated-report-generation
from fpdf import FPDF

# Function to calculate grade based on percentage
def calculate_grade(percentage):
    if percentage >= 90:
        return "A+"
    elif percentage >= 80:
        return "A"
    elif percentage >= 70:
        return "B"
    elif percentage >= 60:
        return "C"
    elif percentage >= 50:
        return "D"
    else:
        return "F"

# Function to generate PDF report
def generate_pdf_report(total_marks, average_percentage, grade):
    pdf = FPDF()
    pdf.add_page()
    pdf.set_font("Arial", size=12)

    pdf.cell(200, 10, txt="Student Report Card", ln=True, align='C')
    pdf.ln(10)
    pdf.cell(200, 10, txt=f"Total Marks: {total_marks}", ln=True)
    pdf.cell(200, 10, txt=f"Average Percentage: {average_percentage:.2f}%", ln=True)
    pdf.cell(200, 10, txt=f"Grade: {grade}", ln=True)

    pdf.output("report_card.pdf")
    print("\n✅ Report card has been generated as 'report_card.pdf'.")

# Main function
def main():
    try:
        subjects = int(input("Enter the number of subjects: "))
        if subjects <= 0:
            print("❌ Please enter a valid number of subjects (greater than 0).")
            return

        marks = []

        for i in range(subjects):
            score = float(input(f"Enter marks obtained in subject {i+1} (out of 100): "))
            if score < 0 or score > 100:
                print("❌ Please enter a valid score between 0 and 100.")
                return
            marks.append(score)

        total_marks = sum(marks)
        average_percentage = total_marks / subjects
        grade = calculate_grade(average_percentage)

        print("\n--- Report Card ---")
        print(f"Total Marks: {total_marks}")
        print(f"Average Percentage: {average_percentage:.2f}%")
        print(f"Grade: {grade}")

        generate_pdf_report(total_marks, average_percentage, grade)

    except ValueError:
        print("❌ Please enter numeric values only.")

# Run the main function
if __name__ == "__main__":
    main()

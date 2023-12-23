#include <stdio.h>

#define NUM_SUBJECTS 5
#define MAX_NAME_LENGTH 10
#define MAX_STUDENTS 100

typedef struct student {
  char name[MAX_NAME_LENGTH];
  int rollno;
  char gender;
  int marks[NUM_SUBJECTS];
  float gpa;
  char grades[NUM_SUBJECTS];
} stud;

stud calculate_grades(stud s);

int main(void) {
  int n, i, j;

  printf("Enter Number of students:");
  scanf("%d", &n);

  if (n <= 0 || n > MAX_STUDENTS) {
    printf("Invalid number of students.\n");
    return 1;
  }

  stud students[MAX_STUDENTS];

  printf("\nSTUDENTS DETAIL\n");

  for (i = 0; i < n; i++) {
    printf("STUDENT_%d:\n", i + 1);

    printf("Name:\n");
    scanf("%s", students[i].name);

    printf("Roll Number:\n");
    scanf("%d", &students[i].rollno);

    printf("Gender(M/F):\n");
    scanf(" %c", &students[i].gender);

    printf("\n\tMarks\n");

    int sum = 0;
    for (j = 0; j < NUM_SUBJECTS; j++) {
      printf("SUBJECT _%d:\n", j + 1);
      scanf("%d", &students[i].marks[j]);
      sum += students[i].marks[j];
    }

    float average = (float)sum / NUM_SUBJECTS;
    students[i].gpa = average;

    students[i] = calculate_grades(students[i]);
  }

  printf("\nSTUDENT DETAILS, GPA, and GRADES\n");
  for (i = 0; i < n; i++) {
    printf("\n");
    printf("STUDENT_%d\n", i + 1);
    printf("Name: %s\n", students[i].name);
    printf("Roll Number: %d\n", students[i].rollno);
    printf("Gender: %c\n", students[i].gender);
    printf("GPA: %.2f\n", students[i].gpa);

    printf("Grades: ");
    for (j = 0; j < NUM_SUBJECTS; j++) {
      printf("%c ", students[i].grades[j]);
    }
    printf("\n");
  }

  return 0;
}

stud calculate_grades(stud s) {
  for (int i = 0; i < NUM_SUBJECTS; i++) {
    if (s.marks[i] >= 90 && s.marks[i] <= 100)
      s.grades[i] = 'A';
    else if (s.marks[i] >= 80 && s.marks[i] < 90)
      s.grades[i] = 'B';
    else if (s.marks[i] >= 70 && s.marks[i] < 80)
      s.grades[i] = 'C';
    else if (s.marks[i] >= 60 && s.marks[i] < 70)
      s.grades[i] = 'D';
    else
      s.grades[i] = 'F';
  }
  return s;
}

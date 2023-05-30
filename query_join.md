# Query con JOIN

### Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```sql
    SELECT * 
    FROM `degrees`
    JOIN `students`
    ON degrees.id = students.degree_id
    WHERE degrees.name LIKE 'Corso di Laurea in Economia';
```

### Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
    SELECT * 
    FROM `departments`
    JOIN `degrees`
    ON departments.id = degrees.department_id
    WHERE departments.name LIKE 'Dipartimento di Neuroscienze' 
    AND degrees.name LIKE 'Corso di Laurea Magistrale%';
```

### Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
    SELECT * 
    FROM `courses`
    JOIN `course_teacher`
    ON courses.id = course_teacher.course_id
    JOIN `teachers`
    ON teachers.id = course_teacher.teacher_id
    WHERE teachers.name = 'Fulvio' 
    AND teachers.surname = 'Amato';
```

### Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
    SELECT students.surname, students.name, degrees.name, departments.name
    FROM `students`
    JOIN `degrees`
    ON degrees.id = students.degree_id
    JOIN `departments`
    ON departments.id = degrees.department_id
    ORDER BY students.surname;
```

### Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
    SELECT degrees.name AS Corso_di_Laurea, courses.name AS Nome_del_Corso, teachers.surname AS Cognome_Insegnante, teachers.name AS Nome_Insegnante
    FROM `degrees`
    JOIN `courses`
    ON degrees.id = courses.degree_id
    JOIN `course_teacher`
    ON courses.id = course_teacher.teacher_id
    JOIN `teachers`
    ON teachers.id = course_teacher.teacher_id;
```

### Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica
```sql
    SELECT departments.name as Nome_dipartimento, teachers.surname AS Cognome_docente, teachers.name AS Nome_docente
    FROM `teachers`
    JOIN `course_teacher`
    ON teachers.id = course_teacher.teacher_id
    JOIN `courses`
    ON courses.id = course_teacher.course_id
    JOIN `degrees`
    ON degrees.id = courses.degree_id
    JOIN `departments`
    ON departments.id = degrees.department_id
    WHERE departments.name = 'Dipartimento di Matematica';
```

### BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
- Senza filtro "voto minimo 18"
```sql
    SELECT students.surname AS Cognome_Studente, students.name AS Nome_Studente, courses.name AS Esame_Sostenuto, MAX(exam_student.vote)AS Voto_Max, COUNT(*) AS `Numero_di_Tentativi`
    FROM `exam_student`
    JOIN students
    ON students.id = exam_student.student_id
    JOIN exams
    ON exams.id = exam_student.exam_id
    JOIN courses
    ON courses.id = exams.course_id
    GROUP BY courses.name, students.surname, students.name   
    ORDER BY `cognome_studente` ASC;
```
- Con filtro "voto minimo 18" (aggiunta del WHERE)
```sql
    SELECT students.surname AS Cognome_Studente, students.name AS Nome_Studente, courses.name AS Esame_Sostenuto, MAX(exam_student.vote)AS Voto_Max, COUNT(*) AS `Numero_di_Tentativi`
    FROM `exam_student`
    JOIN students
    ON students.id = exam_student.student_id
    JOIN exams
    ON exams.id = exam_student.exam_id
    JOIN courses
    ON courses.id = exams.course_id
    WHERE exam_student.vote >= 18
    GROUP BY courses.name, students.surname, students.name   
    ORDER BY `cognome_studente` ASC;
```
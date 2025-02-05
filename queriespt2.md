1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

**SELECT students.name AS student_name, students.surname AS student_surname
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di laurea in economia'**

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

***SELECT departments.name AS department_name, degrees.*
FROM degrees
JOIN departments ON departments.id = degrees.department_id
WHERE departments.name = 'Dipartimento di Neuroscienze'
AND degrees.level = 'magistrale';**

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

**SELECT teachers.id, teachers.name, teachers.surname, courses.name, courses.period
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON teachers.id = course_teacher.teacher_id
WHERE teachers.name = 'Fulvio' AND teachers.surname = "Amato";**


4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

**SELECT students.name, students.surname, degrees.name AS course_name, departments.name AS department_name
FROM students
JOIN degrees ON degrees.id = students.degree_id
JOIN departments ON departments.id = degrees.department_id
ORDER BY students.surname, students.name;**

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

***SELECT degrees.name AS degree_course, teachers.name AS teacher_name, teachers.surname AS teacher_surname, courses.*
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON teachers.id = course_teacher.teacher_id**

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

***SELECT DISTINCT teachers.*
FROM teachers
JOIN course_teacher ON teachers.id = course_teacher.teacher_id
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Matematica';**

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

**SELECT students.name, students.surname, COUNT(exam_student.vote) AS try, MAX(exam_student.vote) AS max_vote
FROM students
JOIN exam_student ON students.id = exam_student.student_id
JOIN exams ON exam_student.exam_id = exams.id
JOIN courses ON courses.id = exams.course_id
GROUP BY students.id, courses.id
HAVING max_vote >= 18**
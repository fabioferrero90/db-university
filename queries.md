## QUERY CON GROUP

1. Contare quanti iscritti ci sono stati ogni anno


**SELECT YEAR(enrolment_date) AS year, 
COUNT(*) AS enrolment_count
FROM students
GROUP BY YEAR(enrolment_date)
ORDER BY YEAR(enrolment_date);**


2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

**SELECT office_address, 
COUNT(*) AS teacher_count
FROM teachers
GROUP BY office_address
ORDER BY teacher_count DESC;**

3. Calcolare la media dei voti di ogni appello d'esame

**SELECT exam_id, AVG(vote) AS average_vote
FROM exam_student
GROUP BY exam_id
ORDER BY exam_id;**

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

**SELECT department_id, 
COUNT(*) AS degree_count
FROM degrees
GROUP BY department_id
ORDER BY department_id;**

## QUERY CON SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)

**SELECT *
FROM students
WHERE YEAR(date_of_birth) = 1990;**

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

**SELECT *
FROM courses
WHERE cfu > 10;**

3. Selezionare tutti gli studenti che hanno più di 30 anni

**SELECT *
FROM students
WHERE YEAR(date_of_birth) <= YEAR(CURDATE()) - 30;**

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

**SELECT *
FROM courses
WHERE year = 1 AND period = 'I semestre';**

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

**SELECT *
FROM exams
WHERE date = '2020-06-20' AND HOUR(hour) >= 14;**


6. Selezionare tutti i corsi di laurea magistrale (38)

**SELECT *
FROM degrees
WHERE NAME LIKE '%Magistrale%'**

7. Da quanti dipartimenti è composta l'università? (12)

**SELECT COUNT(*)
FROM departments**

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

**SELECT COUNT(*)
FROM teachers
WHERE phone IS NULL**

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
degree_id, inserire un valore casuale)

**INSERT INTO students (
    degree_id, 
    name, 
    surname, 
    date_of_birth, 
    fiscal_code, 
    enrolment_date, 
    registration_number, 
    email
)
VALUES (
    FLOOR(RAND() * 75) + 1,
    'Fabio', 
    'Ferrero', 
    '1990-09-26', 
    'FRRFBA90P26E372D', 
    '2024-10-09', 
    137, 
    'fabio.ff90@gmail.com'
);**


10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

**UPDATE teachers
SET office_number = 126
WHERE name = 'Pietro' AND surname = 'Rizzo';**


11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

**DELETE FROM students
WHERE name = 'Fabio' AND surname = 'Ferrero' AND registration_number = 137;**
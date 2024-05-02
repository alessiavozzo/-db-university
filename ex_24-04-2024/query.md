### Selezionare tutti gli studenti nati nel 1990 (160)
- SELECT * FROM `students` WHERE YEAR(date_of_birth) = 1990;
- SELECT * FROM `students` WHERE `date_of_birth` LIKE "1990-%";

### Selezionare tutti i corsi che valgono più di 10 crediti (479)
- SELECT * FROM `courses` WHERE `cfu` > 10;

### Selezionare tutti gli studenti che hanno più di 30 anni
- SELECT * FROM `students` WHERE `date_of_birth` < "1994-04-24";
- SELECT * FROM `students` WHERE `date_of_birth` < DATE_SUB(CURDATE(), INTERVAL 30 YEAR);

#### meno precisi:
- SELECT * FROM `students` WHERE YEAR(date_of_birth) < 1994;
- SELECT * FROM `students` WHERE YEAR(CURDATE()) - YEAR(date_of_birth) > 30;

### Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
- SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = 1;

### Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
- SELECT * FROM `exams` WHERE `date` = "2020-06-20" AND `hour` >= "14:00";

### Selezionare tutti i corsi di laurea magistrale (38)
- SELECT * FROM `degrees` WHERE `level`= "magistrale";

### Da quanti dipartimenti è composta l'università? (12)
- SELECT COUNT(*) as `n_departments` FROM `departments`;

### Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
- SELECT COUNT(*) AS `teachers_without_phone_number` FROM `teachers` WHERE `phone` IS NULL;

# FATTI IN CLASSE 02/05/2024

### Selezionare tutti i corsi del Corso di Laurea in Informatica (22)
- SELECT `courses`.`name`,`courses`.`year`,`courses`.`website`,`degrees`.`name` AS `degree_name` FROM `courses` JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` WHERE `degrees`.`name`= "Corso di Laurea in Informatica";

###  Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame
- SELECT `courses`.`id`,`courses`.`name`,`courses`.`description`,`courses`.`period`,`courses`.`year`,`courses`.`cfu`,`courses`.`website`,`exams`.`*`
FROM `courses`
INNER JOIN `exams` ON `courses`.`id` = `exams`.`course_id`
WHERE `courses`.`id` = 144;

###  Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)
- SELECT `departments`.`*`
FROM `departments`
JOIN `degrees`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Diritto dell'Economia";

### 
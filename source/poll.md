```
Release 0:

1)

INSERT INTO voters
(first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
VALUES
('Aditya', 'Mahesh', 'Male', 'Democrat', 5, 22, ‘No’, '0', 'No', 'No', DATETIME('now'), DATETIME('now'));

INSERT INTO voters
(first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
VALUES
(‘Rick, ‘Rubio’, 'Male', 'Democrat', 5, 22, ‘No’, '0', 'No', 'No', DATETIME('now'), DATETIME('now'));

INSERT INTO votes
(voter_id, politician_id, created_at, updated_at)
VALUES
(5001, 499,  DATETIME('now'), DATETIME('now’));

INSERT INTO votes
(voter_id, politician_id, created_at, updated_at)
VALUES
(5002, 145,  DATETIME('now'), DATETIME('now’));

2)

SELECT * FROM congress_members WHERE location = 'NJ’;
UPDATE congress_members SET name='Donald Trump' WHERE id=102;

Release 1:

1)

DELETE FROM voters WHERE party NOT IN ('democrat', 'republican', 'Democrat');

2)

DELETE FROM votes
WHERE votes.voter_id IN (SELECT voters. id FROM votes JOIN congress_members ON votes.politician_id = congress_members.id
join voters on voters.id = votes.voter_id
WHERE congress_members.grade_current > 12 and voters.homeowner = 1 and voters.employed = 1 and voters.children_count = 0 and party_duration < 3
GROUP BY votes.voter_id);

DELETE FROM voters
WHERE voters.id IN (196, 2038, 3004, 4210);

Release 2:

1)

UPDATE votes SET politician_id = 346 Where votes.id IN (SELECT votes.id from voters join votes on voters.id = voter_id
WHERE voters.age > 80 and voters.gender = 'male' and voters.children_count = 0);

2)

dude with the highest id = 530

SELECT congress_members.id FROM congress_members
ORDER BY grade_1996 DESC
LIMIT 1;

dude with the lowest id = 1

SELECT congress_members.id FROM congress_members
ORDER BY grade_1996 ASC
LIMIT 1;

the number of votes the dude with the highest speaking score has

SELECT COUNT(votes.id) FROM votes
WHERE politician_id = (SELECT congress_members.id FROM congress_members
ORDER BY grade_1996 DESC
LIMIT 1);

the number of votes the dude with lowest score has = 15

SELECT COUNT(votes.id) FROM votes
WHERE politician_id = (SELECT congress_members.id FROM congress_members
ORDER BY grade_1996 ASC
LIMIT 1);

give the votes to the dude with the lowest score

UPDATE votes SET politician_id = 346 Where votes.id IN (SELECT votes.id from voters join votes on voters.id = voter_id
WHERE voters.age > 80 and voters.gender = 'male' and voters.children_count = 0);

UPDATE votes SET politician_id = 1 WHERE politician_id = 530;
```
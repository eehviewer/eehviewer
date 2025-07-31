
CREATE TABLE users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role ENUM('admin', 'teacher', 'student') NOT NULL,
    created_at ti meSTAMP DEFAULT CURRENT_ti meSTAMP
);
 
-- 题目表
CREATE TABLE questions (
    question_id INT PRIMARY KEY AUTO_INCREMENT,
    content TEXT NOT NULL,
    type ENUM('single_choice', 'multiple_choice', 'true_false', 'short_answer', 'essay') NOT NULL,
    difficulty DECIMAL(3,2) CHECK (difficulty BETWEEN 0 AND 1),
    creator_id INT NOT NULL,
    created_at ti meSTAMP DEFAULT CURRENT_ti meSTAMP,
    FOREIGN KEY (creator_id) REFERENCES users(user_id)
);
 
-- 选项表（适用于选择题）
CREATE TABLE options (
    option_id INT PRIMARY KEY AUTO_INCREMENT,
    question_id INT NOT NULL,
    content TEXT NOT NULL,
    is_correct BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (question_id) REFERENCES questions(question_id) ON DELETE CASCADE
);
 
-- 试卷表
CREATE TABLE exams (
    exam_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    description TEXT,
    duration INT COMMENT '考试时长(分钟)',
    creator_id INT NOT NULL,
    created_at ti meSTAMP DEFAULT CURRENT_ti meSTAMP,
    FOREIGN KEY (creator_id) REFERENCES users(user_id)
);

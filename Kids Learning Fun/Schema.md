```sql
-- ===============================
-- CORE ACCOUNTS
-- ===============================

CREATE TABLE parent (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE kid (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    parent_id BIGINT NOT NULL,
    name VARCHAR(100),
    age INT,
    grade VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_kid_parent FOREIGN KEY (parent_id) REFERENCES parent(id)
);

-- ===============================
-- LEARNING CONTENT
-- ===============================

CREATE TABLE subject (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE topic (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    subject_id BIGINT NOT NULL,
    name VARCHAR(100) NOT NULL,
    display_order INT,
    CONSTRAINT fk_topic_subject FOREIGN KEY (subject_id) REFERENCES subject(id)
);

CREATE TABLE question (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    topic_id BIGINT NOT NULL,
    difficulty INT NOT NULL,
    question_text VARCHAR(500),
    correct_answer VARCHAR(255),
    CONSTRAINT fk_question_topic FOREIGN KEY (topic_id) REFERENCES topic(id)
);

-- ===============================
-- PARENT CONTROL
-- ===============================

CREATE TABLE parent_topic_settings (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    parent_id BIGINT NOT NULL,
    kid_id BIGINT NOT NULL,
    topic_id BIGINT NOT NULL,
    enabled BOOLEAN DEFAULT TRUE,
    min_difficulty INT,
    max_difficulty INT,
    adaptive_enabled BOOLEAN DEFAULT TRUE,
    CONSTRAINT fk_pts_parent FOREIGN KEY (parent_id) REFERENCES parent(id),
    CONSTRAINT fk_pts_kid FOREIGN KEY (kid_id) REFERENCES kid(id),
    CONSTRAINT fk_pts_topic FOREIGN KEY (topic_id) REFERENCES topic(id),
    CONSTRAINT uq_parent_kid_topic UNIQUE (parent_id, kid_id, topic_id)
);

-- ===============================
-- LEARNING RUNTIME
-- ===============================

CREATE TABLE learning_session (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    kid_id BIGINT NOT NULL,
    subject_id BIGINT NOT NULL,
    start_time TIMESTAMP,
    end_time TIMESTAMP,
    CONSTRAINT fk_session_kid FOREIGN KEY (kid_id) REFERENCES kid(id),
    CONSTRAINT fk_session_subject FOREIGN KEY (subject_id) REFERENCES subject(id)
);

CREATE TABLE attempt (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    session_id BIGINT NOT NULL,
    question_id BIGINT NOT NULL,
    given_answer VARCHAR(255),
    correct BOOLEAN,
    time_taken_ms BIGINT,
    attempted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_attempt_session FOREIGN KEY (session_id) REFERENCES learning_session(id),
    CONSTRAINT fk_attempt_question FOREIGN KEY (question_id) REFERENCES question(id)
);

-- ===============================
-- PROGRESS & ANALYTICS
-- ===============================

CREATE TABLE topic_progress (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    kid_id BIGINT NOT NULL,
    topic_id BIGINT NOT NULL,
    total_attempts INT DEFAULT 0,
    correct_attempts INT DEFAULT 0,
    accuracy DOUBLE,
    mastery_level VARCHAR(30),
    current_difficulty INT,
    last_updated TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_progress_kid FOREIGN KEY (kid_id) REFERENCES kid(id),
    CONSTRAINT fk_progress_topic FOREIGN KEY (topic_id) REFERENCES topic(id),
    CONSTRAINT uq_kid_topic UNIQUE (kid_id, topic_id)
);

CREATE TABLE analytics_snapshot (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    kid_id BIGINT NOT NULL,
    snapshot_date DATE,
    total_time_minutes INT,
    total_attempts INT,
    correct_attempts INT,
    accuracy DOUBLE,
    CONSTRAINT fk_snapshot_kid FOREIGN KEY (kid_id) REFERENCES kid(id)
);

-- ===============================
-- RECOMMENDATIONS
-- ===============================

CREATE TABLE recommendation (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    parent_id BIGINT NOT NULL,
    kid_id BIGINT NOT NULL,
    topic_id BIGINT,
    message VARCHAR(500),
    priority INT,
    status VARCHAR(30),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_rec_parent FOREIGN KEY (parent_id) REFERENCES parent(id),
    CONSTRAINT fk_rec_kid FOREIGN KEY (kid_id) REFERENCES kid(id),
    CONSTRAINT fk_rec_topic FOREIGN KEY (topic_id) REFERENCES topic(id)
);

CREATE TABLE recommendation_reason (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    recommendation_id BIGINT NOT NULL,
    metric VARCHAR(50),
    metric_value DOUBLE,
    threshold DOUBLE,
    CONSTRAINT fk_reason_rec FOREIGN KEY (recommendation_id) REFERENCES recommendation(id)
);

```
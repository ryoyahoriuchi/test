# README

# STEP1 assumption_table_schema
```rb
create_table "users", force: :cascade do |t|  
  t.string "name"  
  t.string "email"  
  t.string "password_digest"  
  t.index ["email"], name: "index_users_on_email", unique: true  
end  
  
create_table "tasks", force: :cascade do |t|  
  t.string "name"  
  t.text "explanation"  
  t.integer "deadline"  
  t.string "progress"  
  t.integer "priority"  
  t.index ["user_id"], name: "index_tasks_on_user_id"  
end  
  
create_table "labels", force: :cascade do |t|  
  t.string "name"  
  t.index ["task_id"], name: "index_labels_on_tasks_id"  
end  
  
add_foreign_key "tasks", "users"  
add_foreign_key "labels", "tasks"  

```
# User
|  カラム名         | データ型 |
|------------------|---------|
| name             | string  |
| email            | string  |
| password_digest  | string  |

# Task
| カラム名      | データ型  |
|--------------|----------|
| name         | string   |
| explanation  | text     |
| deadline     | integer  |
| progress     | string   |
| priority     | integer  |
| user_id      | index    | 

# Label
| カラム名  | データ型  |
|----------|-----------|
| name     | string    |
| task_id  | index     |

# デプロイの方法
1. $ heroku login
1. $ heroku create
1. ※Ruby2.6.5を使用している場合
    1. 「Gemfile」のruby '2.6.5'をコメントアウトする
    1. $ bundle install
1. $ git add -A
1. $ git commit -m "init"
1. $ heroku buildpacks:set heroku/ruby
1. $ heroku buildpacks:add --index 1 heroku/nodejs
1. $ git push heroku master
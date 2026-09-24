Classmate Board for N1E
上传到 GitHub 的用法（不用 Firebase）

你只需要上传这两个文件：
- index.html
- mascot.png

========================================
A. 先做 Supabase（只要做一次，约 3 分钟）
========================================
1. 打开 https://supabase.com  用邮箱免费注册
2. 点 New project，名字随便，例如 n1e-board
3. 等项目建好后：
   左边点 SQL Editor -> New query
   把下面整段贴进去，点 Run：

create table if not exists messages (
  id bigint generated always as identity primary key,
  user_id uuid not null,
  user_name text not null,
  content text not null,
  created_at timestamptz not null default now()
);

alter table messages enable row level security;

create policy "classmates can read" on messages
  for select to authenticated using (true);

create policy "classmates can insert own" on messages
  for insert to authenticated with check (auth.uid() = user_id);

4. 左边 Authentication -> Providers
   确认 Email 是打开的（默认是开的）
   如果有 “Confirm email”，可以先关掉，这样小朋友注册后马上能进

5. 左边 Project Settings（齿轮）-> API
   复制这两样：
   - Project URL
   - anon public  key

6. 用记事本打开 index.html，找到最上面这两行，贴进去：

   const SUPABASE_URL = "https://xxxx.supabase.co";
   const SUPABASE_ANON_KEY = "eyJ....";

   保存。

========================================
B. 上传到 GitHub，变成网页
========================================
1. 打开 https://github.com 登录（没有就注册）
2. 右上角 +  -> New repository
   名字例如：n1e-board
   选 Public
   不要勾 README
   点 Create repository
3. 页面上有 “uploading an existing file”
   把 index.html 和 mascot.png 两个一起拖进去
   点 Commit changes
4. 打开仓库 Settings -> Pages
   Source 选 Deploy from a branch
   Branch 选 main，文件夹 / (root)
   点 Save
5. 等 1 分钟，同一页会出现网址，例如：
   https://你的用户名.github.io/n1e-board/
6. 用手机打开这个网址试一下 Register。
   成功后把这个网址发给同学。

========================================
C. 同学怎么用
========================================
打开你的 GitHub 网页 -> Register
填：真名 + 邮箱 + 密码（至少 6 位）
然后就可以留言。大家看到的是同一个留言板。

注意：两个文件要放在同一层，不要把 mascot.png 放进子文件夹。

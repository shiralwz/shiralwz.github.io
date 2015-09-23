---
layout: post
title:  "Rails 应用使用 Capistrano2 部署流程"
date:   2015-09-22 15:08:25
categories: Capistrano2
---
Capistrano 2 首次部署流程

    modify config/deploy.rb and config/deploy/production.rb
    bundle exec cap production deploy:setup
    bundle exec cap production deploy:check
    bundle exec cap production deploy:cold

配置 Nginx

    ln -s /opt/app/ruby/aaa-cms/current/config/nginx.conf /etc/nginx/conf.d/ott_tv_cms.conf
    添加 “include conf.d/aaa_cms.conf;” 到 /etc/nginx/nginx.conf
    运行 nginx -t 来检查 nginx 配置没有问题
    运行 nginx -s reload 来重启 nginx

初始话数据库数据

    RAILS_ENV=production bundle exec bin/rake db:seed

Capistrano 2 首次部署完成后再部署

   bundle exec cap production deploy

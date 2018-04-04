### 在emacs中开发python
直接看代码 [点击查看自用配置详情](https://github.com/sunhuachuang/emacs.d/blob/master/lisp/init-python-mode.el)

```lisp
(setq auto-mode-alist
      (append '(("SConstruct\\'" . python-mode)
                ("SConscript\\'" . python-mode))
              auto-mode-alist))

(require-package 'pip-requirements)

;; flycheck use python flake8
;; pip install flake8  => C-c ! s
(when (maybe-require-package 'anaconda-mode)
  (after-load 'python
    (add-hook 'python-mode-hook 'anaconda-mode)
    (add-hook 'python-mode-hook 'anaconda-eldoc-mode))
  (when (maybe-require-package 'company-anaconda)
    (after-load 'company
      (add-hook 'python-mode-hook
                (lambda () (sanityinc/local-push-company-backend 'company-anaconda))))))

;; auto pep8 style format
;; need pip install autopep8
(defcustom python-autopep8-path (executable-find "autopep8")
  "Autopep8 executable path."
  :group 'python
  :type 'string)

(defun python-autopep8 ()
  "Automatically formats Python code to conform to the PEP 8 style guide.
$ autopep8 --in-place --aggressive --aggressive <filename>"
  (interactive)
  (when (eq major-mode 'python-mode)
    (shell-command
     (format "%s --in-place --aggressive %s" python-autopep8-path
             (shell-quote-argument (buffer-file-name))))
    (revert-buffer t t t)))

(eval-after-load 'python
  '(if python-autopep8-path
       (add-hook 'after-save-hook 'python-autopep8)))

(provide 'init-python-mode)

```
#### 注意点
1. 因为emacs的配置是fork自purcell的基础配置，所以外部不作介绍，就看python的配置
2. 外部需要安装的pip包 有: flake8 (检查代码规范), autopep8 (格式化代码)
3. 主体的python环境用的是anaconda包，并且使用comapany-anaconda来完成自动补全，保存时候自动进行pep8的format操作
4. 关于autopep8 如果format一个文件夹而不是单个文件，在外部命令行下执行 `autopep8 --in-place --recursive your_dir`
5. 如丝般润滑~

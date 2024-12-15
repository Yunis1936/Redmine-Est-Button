// ==UserScript==
// @name         Redmine Est Button
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Добавляет кнопку Est в панель инструментов редакторов задач и комментариев на Redmine.
// @author       Ты
// @match        https://redmine.lachestry.tech/*
// @match        https://redmine.rigla.ru/*
// @icon         https://www.redmine.org/favicon.ico
// @grant        none
// ==/UserScript==

(function () {
    'use strict';

    function addEstButton(toolbar, textarea) {
        if (!toolbar || !textarea) {
            return;
        }

        // Проверка на наличие кнопки, чтобы не дублировать
        if (toolbar.querySelector('.jstb_est')) {
            return;
        }

        const estButton = document.createElement('button');
        estButton.type = 'button';
        estButton.className = 'jstb_est';
        estButton.title = 'Добавить оценку';

        // Стили кнопки
        Object.assign(estButton.style, {
            marginRight: '2px',
            width: '24px',   // Размер кнопки
            height: '24px',
            padding: '0',
            borderStyle: 'solid',
            borderWidth: '1px',
            borderColor: '#ddd',
            backgroundColor: 'transparent',
            backgroundImage: 'url("https://as2.ftcdn.net/v2/jpg/01/27/01/55/1000_F_127015517_rD10cUNAuo3NZsvHvCqygoY06HaU8evp.jpg")', // URL иконки кнопки
            backgroundSize: 'cover',
            backgroundPosition: 'center',
            cursor: 'pointer',
            opacity: '1',
        });

        // Логика кнопки
        estButton.addEventListener('click', function () {
            const textToInsert =
                '*Оценка:*\n\n* Аналитика - \n* Разработка - \n* Тестирование - \n\n*Итого: *\n';
            const selectionStart = textarea.selectionStart;

            textarea.value =
                textarea.value.substring(0, selectionStart) +
                textToInsert +
                textarea.value.substring(selectionStart);

            textarea.setSelectionRange(
                selectionStart,
                selectionStart + textToInsert.length
            );
            textarea.focus();
        });

        toolbar.appendChild(estButton);
    }

    function initEstButton() {
        const descriptionToolbar = document.querySelector('.jstElements');
        const descriptionTextarea = document.querySelector('#issue_description');
        if (descriptionToolbar && descriptionTextarea) {
            addEstButton(descriptionToolbar, descriptionTextarea);
        }

        const commentToolbar = document.querySelectorAll('.jstElements')[1];
        const commentTextarea = document.querySelector('#issue_notes');
        if (commentToolbar && commentTextarea) {
            addEstButton(commentToolbar, commentTextarea);
        }
    }

    // Наблюдатель за изменениями DOM
    const observer = new MutationObserver(initEstButton);
    observer.observe(document.body, { childList: true, subtree: true });
})();

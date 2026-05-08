一个校园网自动登录脚本

// ==UserScript==
// @name         校园网自动登录（深澜认证）
// @namespace    http://tampermonkey.net/
// @version      5.0
// @description  打开校园网登录页自动填入账号密码并登录，支持电信/移动/联通
// @author       Claude AI
// @match        http://172.29.0.2/*
// @grant        none
// ==/UserScript==
(function() {
    'use strict';
    // ============================================================
    //  👇 只改下面三行！👇
    // ============================================================
    const ACCOUNT  = '你的学号';       // ← 改成学工号
    const PASSWORD = '你的密码';       // ← 改成密码
    const ISP      = '@telecom';      // ← @telecom / @cmcc / @unicom
    // ============================================================
    //  👆 只改上面三行！👆
    // ============================================================
    function fillAndLogin() {
        const userField = document.querySelector('input[name="DDDDD"][type="text"]');
        const passField = document.querySelector('input[name="upass"][type="password"]');
        const ispSelect = document.querySelector('select[name="ISP_select"]');
        const loginBtn  = document.querySelector('input[name="0MKKey"][type="button"]');
        if (!userField || !passField || !ispSelect || !loginBtn) {
            setTimeout(fillAndLogin, 1000);
            return;
        }
        // 填账号
        userField.focus();
        userField.value = ACCOUNT;
        userField.dispatchEvent(new Event('input', { bubbles: true }));
        userField.dispatchEvent(new Event('change', { bubbles: true }));
        // 填密码
        passField.focus();
        passField.value = PASSWORD;
        passField.dispatchEvent(new Event('input', { bubbles: true }));
        passField.dispatchEvent(new Event('change', { bubbles: true }));
        // 选运营商
        ispSelect.value = ISP;
        ispSelect.dispatchEvent(new Event('change', { bubbles: true }));
        // 点登录
        setTimeout(() => loginBtn.click(), 400);
    }
    setTimeout(fillAndLogin, 1500);
})();

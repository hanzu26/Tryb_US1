#!/usr/bin/env python
*** Settings ***
Library    SeleniumLibrary

*** Variables ***
${url}          https://dev.tryb.ai/login
${browser}      chrome
${email}        trainee.two@example.user
${passwort}     test12345
${InputBox}     xpath://*[@id="main"]/app-quest-page/div/div/div/div[2]/app-context-menu/div/div[1]/form/div/input
${IM}           xpath://*[@id="main"]/app-quest-page/div/div/div/div[2]/app-context-menu/div/div[1]/div

*** Test Cases ***
Start

    Log In
    New Project DE
DefaultCheck

    textfield should contain    ${InputBox}    Neues Training
CloneDefaultCheck

    Verify Name of Clone DE
ErrorMessage_NoInput

    Press Keys      ${InputBox}      CTRL+A+DELETE
    element text should be  ${IM}  Trainingsname eingeben.
ErrorMessage_TooShort

    Verify Short Name DE    a
    Verify Short Name DE    6
    Verify Short Name DE    _
HappyPart

    Verify Valid Name DE    abc
    Verify Valid Name DE    567
    Verify Valid Name DE    -_.
    Verify Valid Name DE    Deutschland Nürnberg
ErrorMessage_MinMax

    Verify Valid Name DE    a2
    Verify Valid Name DE    aaaaaaaaaaaaaaaaaaaaaaaaaaaaaa32
ErrorMessage_TooLong

    Verify Long Name DE     aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
    Verify Long Name DE     123456789101112131415161718192021
ErrorMessage_ValidSpecialChar

    Verify Valid Name DE    --
    Verify Valid Name DE    __
    Verify Valid Name DE    ..
    Verify Valid Name DE    1Convit Xoera caiCanh
ErrorMessage_InValidSpecialChar

    Verify Special Characters DE    ?
    Verify Special Characters DE    @
    Verify Special Characters DE    *
CloneChangeCheck

    run keyword and continue on failure     Verify Change Name of Clone DE  Name Änderung
DeleteProjet
    Delete Project DE
    close all browsers


*** Keywords ***
Log In
    open browser    ${url}  ${browser}
    maximize browser window
    set selenium speed    0.2
    input text    name:email     ${email}
    input text    name:password  ${passwort}
    click button    xpath://button[contains(text(),'Einloggen')]
    wait until page contains    Erstelle deinen eigenen Skill
New Project DE
    click element    xpath://*[@id="workspace"]/span
    click element    xpath://*[@id="ngb-nav-0-panel"]/app-project-library/app-card-page/div[1]/app-add-card/div/div[1]/span
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[1]/div/div/div[3]/div/div[2]/img
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[2]/div/div/div[4]/div/div[2]/img
    input text       xpath://*[@id="projectName"]      test_test
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[3]/div/div/form/div/div[2]/button[2]
    #click element    xpath://body/app-root[1]/div[1]/app-workspace[1]/div[1]/div[3]/div[1]/div[1]/app-project-library[1]/app-card-page[1]/div[1]/app-card[1]/div[1]/ngb-carousel[1]/div[2]/div[1]/img[1]
    click element    xpath://*[@id="sticky-sidebar"]/app-project-workspace-navigation/div/div[2]/a[2]/span
New Project EN
    click element    xpath://*[@id="ngb-nav-5-panel"]/app-project-library/app-card-page/div[1]/app-add-card/div/div[1]/span
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[1]/div/div/div[3]/div/div[2]/img
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[2]/div/div/div[4]/div/div[2]/img
    input text       xpath://*[@id="projectName"]      test_test
    click element    xpath://*[@id="project-wizard"]/app-wizard-slide/div[3]/div/div/form/div/div[2]/button[2]
    #click element    xpath://body/app-root[1]/div[1]/app-workspace[1]/div[1]/div[3]/div[1]/div[1]/app-project-library[1]/app-card-page[1]/div[1]/app-card[1]/div[1]/ngb-carousel[1]/div[2]/div[1]/img[1]
    click element    xpath://*[@id="sticky-sidebar"]/app-project-workspace-navigation/div/div[2]/a[2]/span
Delete Project DE
    click element    xpath://*[@id="workspace"]/span
    click element    xpath://*[@id="ngb-nav-5-panel"]/app-project-library/app-card-page/div[1]/app-card[1]/div/div[2]/span
    click element    xpath://*[@id="mat-dialog-0"]/app-confirm-dialog/div[2]/button[1]
Delete Project EN
    click element    xpath://*[@id="workspace"]/span
    click element    xpath://*[@id="ngb-nav-10-panel"]/app-project-library/app-card-page/div[1]/app-card[1]/div/div[2]/span
    click element    xpath://*[@id="mat-dialog-1"]/app-confirm-dialog/div[2]/button[1]
Change Language
    click element    //*[@id="lang"]/div/div[1]/p/mat-icon
    seleniumlibrary.click element    xpath://*[@id="lang"]/div
Verify Short Name DE
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be  ${IM}  Zu kurzer Trainingsname.
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Long Name DE
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be    ${IM}  Zu langer Trainingsname.
    seleniumlibrary.press keys    ${InputBox}        ENTER
    element should not contain    class:training-title    ${Inputname}
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Valid Name DE
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element should not be visible    ${IM}
    click element    //*[@id="split-menu-section"]/div/div[6]/div/div
    element should contain    class:training-title    ${Inputname}
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Special Characters DE
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be    ${IM}  Sonderzeichen nicht erlaubt.
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Name of Clone DE
    open context menu    class:tree-chart-node
    click element    //*[@id="main"]/app-quest-page/div/div/div/div[1]/div/app-tree/div/div/app-right-click-menu/div/button[2]
    textfield should contain    ${InputBox}    Neues Training Klon
    click element       class:tree-chart-node
Verify Change Name of Clone DE
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}       ${Inputname}
    click element    //*[@id="split-menu-section"]/div/div[6]/div/div
    open context menu    class:tree-chart-node
    click element    //*[@id="main"]/app-quest-page/div/div/div/div[1]/div/app-tree/div/div/app-right-click-menu/div/button[2]
    ${Inputname}=   catenate    ${Inputname}    Klon
    textfield should contain    ${InputBox}   ${Inputname}


Verify Short Name EN
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be  ${IM}  Training name is too short.
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Long Name EN
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be    ${IM}  Training name is too long.
    seleniumlibrary.press keys    ${InputBox}        ENTER
    element should not contain    class:training-title    ${Inputname}
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Valid Name EN
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element should not be visible    ${IM}
    click element    //*[@id="split-menu-section"]/div/div[6]/div/div
    element should contain    class:training-title    ${Inputname}
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Special Characters EN
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}     ${Inputname}
    element text should be    ${IM}  Special characters not allowed.
    Press Keys      ${InputBox}       CTRL+A+DELETE
Verify Name of Clone EN
    open context menu    class:tree-chart-node
    click element    //*[@id="main"]/app-quest-page/div/div/div/div[1]/div/app-tree/div/app-right-click-menu/div/button[2]
    textfield should contain    ${InputBox}    New Training Clone
    click element       class:tree-chart-node
Verify Change Name of Clone EN
    wait until element is enabled    ${IM}
    [Arguments]    ${Inputname}
    input text    ${InputBox}       ${Inputname}
    click element    //*[@id="split-menu-section"]/div/div[6]/div/div
    open context menu    class:tree-chart-node
    click element    //*[@id="main"]/app-quest-page/div/div/div/div[1]/div/app-tree/div/app-right-click-menu/div/button[2]
    ${Inputname}=   catenate    ${Inputname}    Clone
    textfield should contain    ${InputBox}   ${Inputname}

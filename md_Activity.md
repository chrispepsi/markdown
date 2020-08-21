### アクティビティ図(フローチャート)

#### アクティビティ図１
~~~plantuml
@startuml

start
:ClickServlet.handleRequest();
:new page;
if (Page.onSecurityCheck) then (true)
  :Page.onInit();
  if (isForward?) then (no)
    :Process controls;
    if (continue processing?) then (no)
      stop
    endif

    if (isPost?) then (yes)
      :Page.onPost();
    else (no)
      :Page.onGet();
    endif
    :Page.onRender();
  endif
else (false)
endif

if (do redirect?) then (yes)
  :redirect process;
else
  if (do forward?) then (yes)
    :Forward request;
  else (no)
    :Render page template;
  endif
endif

stop

@enduml
~~~

#### アクティビティ図２
```plantuml
@startuml

|__顧客__|
    :注文する;

|#AntiqueWhite|__販売部門__|
    :在庫を確認する;
    :出荷を確認する;

|__出荷部門__|
    :出荷する;
    fork
    :出荷を報告する;

|#AntiqueWhite|__経理部門__|
    :請求する;

|__顧客__|
    forkagain
    :商品を受け取る;

|__顧客__|
    end fork
    :支払う;

|#AntiqueWhite|__経理部門__|
    :入金を確認する;

@enduml
```
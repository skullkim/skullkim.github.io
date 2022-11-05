---
layout:       post
title:        "Object pooling"
author:       "yunki kim"
header-style: text
catalog:      true
tags: 
- objectpooling
---

<head></head>
<body id="tt-body-page" class="">
<div id="wrap" class="wrap-right">
    <div id="container">
        <main class="main ">
            <div class="area-main">
                <div class="area-view">
                    <div class="article-header"></div>
                    <hr>
                    <div class="article-view">
                        <div class="contents_style">
                            <p data-ke-size="size16">&nbsp; Garbage collection(GC)은 자동으로 메모리 해제를 해주지만 때때로 원치 않는 메모리를 헤제하거나 지연을 야기할 수 있다. 이는 단시간 내에 객체들을 수 없이 생성하고 없애는 것을 반복할때 일어난다. 이런 현상은 3D렌더링과 프레임당 수 많은 임시 벡터 객체들을 동적할당할때 발생한다.&nbsp;</p>
<p data-ke-size="size16">&nbsp; 이런 현상을 해결기 위해 통상적으로 임시 객체를 생성하는 대신 이미 생성된 객체를 재사용하는 방식을 사용한다. 지금 당장 사용하지 않는 인스턴스들을 위한 pool을 만들고 필요할때 객체들을 pull하면 된다. 이렇게 하면 garbage collector가 헤제 해야할 메모리가 줄어 들기 때문에 garbage colltector가 해야할 일이 줄어든다. 이렇게 되면 객체는 object pool에 존재하거나 사용중이게 된다. object pool은 객체들에 대한 레퍼런스를 가지고 있다</p>
<p data-ke-size="size16">&nbsp; 만약 allocate()가 필요 하다면 object pool에서 우선적으로 해당 객체가 free list에 존재하는지 본다. 존재한다면 free list에서 이 객체를 지우고 이 객체를 반환한다. free()의 경우 해당 객체는 다시 object pool에 넣어진다.</p>
<p data-ke-size="size16">*pool은 재사용될 준비를 하는 자원의 집합을 의미한다</p>
                        </div>
                        <br>
                        <div class="tags"></div>
                    </div>
                    
                </div>
            </div>
        </main>
    </div>
</div>


</body>
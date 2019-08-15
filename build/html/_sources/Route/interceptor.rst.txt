####################################################################################################
**路由拦截器(Interceptor)**
####################################################################################################

******************************************************************************************
**URL**
******************************************************************************************

.. code-block:: php
    :linenos:

    <?php
        class UrlAccessInterceptor implements \CInterceptors
        {
            /**
             * @param CRequest $request
             * @param CNext $next
             * @return CNext|CResponseData
             */
            public function handle(CRequest $request, CNext $next)
            {
                if ($request->getUrl()->getActionStr() == '/special/task/index' && $request->getParams('is_from_pc') == 1) {
                    return new \CRedirectData('/special/architecture/index', [
                        '_is_for_nav' => 1
                    ]);
                }

                return $next;
            }
        }
    ?>


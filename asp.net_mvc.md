## ASP.NET MVC

### 危険性のある入力検証を無効化する  
  デフォルトでタグ文字等の脆弱性の危険性のある文字列はチェックされる。  
  チェックを行わないようにするためには、アクションメソッドに以下の属性を指定する。  
  ```
  [ValidateInput(false)]
  public ActionResult someAction(){...}
  ```
  
### 非Nullableの型の自動クライアント検証を無効化する  
  デフォルトでは非Nullableの型のプロパティに対してクライアント検証のコードが埋め込まれる。  
  これを回避するには以下の方法がある。  
  （方法１）Webプロジェクト全体に設定する。  
  ```
  ModelValidatorProviders.Providers.Clear();
  ModelValidatorProviders.Providers.Add(new DataAnnotationsModelValidatorProvider());
  DataAnnotationsModelValidatorProvider.AddImplicitRequiredAttributeForValueTypes = false;
  ```

  （方法２）リクエストごとに無効化する。  
  　画面（cshtml）にて、クライアントチェックが不要な個所を以下のコードで挟む。
  ```
  @{ Html.EnableClientValidation(false); }
  @{ Html.EnableClientValidation(true); }
  ```

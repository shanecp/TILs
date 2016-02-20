## Angular-checklist-model with ion-checklist

Using [Angular-checklist-model](https://github.com/vitalets/checklist-model) with Ionic checklist.

```
			<ion-list>
				<ion-item class="item-checkbox" ng-repeat="roles in roleTypes">
					<label class="checkbox">
						<input type="checkbox"
							   checklist-model="auth.roles"
							   data-checklist-value="role" />
					</label>
					{{ role.name }}
				</ion-item>
			</ion-list>
```
